<template>
	<view :class="['cy-upload', customClass]">
		<view class="cy-upload__title" v-if="title">{{ title }}</view>

		<upload-image v-if="fileMediatype === 'image' && showType === 'grid'"
					  :readonly="readonly"
					  :files-list="filesList"
					  :limit="limitLength"
					  :disablePreview="disablePreview"
					  :delIcon="delIcon"
					  @uploadFiles="uploadFiles"
					  @choose="choose"
					  @delFile="delFile">
			<slot>
				<cy-icon name="add-line" />
			</slot>
		</upload-image>

		<upload-file v-if="fileMediatype !== 'image' || showType !== 'grid'"
					 :readonly="readonly"
					 :files-list="filesList"
					 :showType="showType"
					 :delIcon="delIcon"
					 @uploadFiles="uploadFiles"
					 @choose="choose"
					 @delFile="delFile">
			<slot>
				<cy-button theme="primary">选择文件</cy-button>
			</slot>
		</upload-file>
	</view>
</template>

<script>
import {
	chooseAndUploadFile,
	uploadCloudFiles
} from './upload-file.js'
import {
	get_file_ext,
	get_extname,
	get_files_and_is_max,
	get_file_info,
	get_file_data
} from './utils.js'

import uploadImage from './upload-image.vue'
import uploadFile from './upload-file.vue'

let fileInput = null

export default {
	name: "upload",
	components: {
		uploadImage,
		uploadFile
	},
	externalClasses: ['custom-class'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	emits: ['select', 'success', 'fail', 'progress', 'delete', 'update:modelValue', 'input'],
	props: {
		title: {
			type: String,
		},
		modelValue: {
			type: [Array, Object],
			default() {
				return []
			}
		},
		value: {
			type: [Array, Object],
			default() {
				return []
			}
		},
		disabled: {
			type: Boolean,
			default: false
		},
		disablePreview: {
			type: Boolean,
			default: false
		},
		delIcon: {
			type: Boolean,
			default: true
		},
		// 自动上传
		autoUpload: {
			type: Boolean,
			default: true
		},
		// 最大选择个数 ，h5只能限制单选或是多选
		limit: {
			type: [Number, String],
			default: 9
		},
		// 列表样式 grid | list | list-card
		mode: {
			type: String,
			default: 'grid'
		},
		// 选择文件类型  image/video/all
		fileMediatype: {
			type: String,
			default: 'image'
		},
		// 文件类型筛选
		fileExtname: {
			type: [Array, String],
			default() {
				return []
			}
		},
		title: {
			type: String,
			default: ''
		},
		listStyles: {
			type: Object,
			default() {
				return {
					// 是否显示边框
					border: true,
					// 是否显示分隔线
					dividline: true,
					// 线条样式
					borderStyle: {}
				}
			}
		},
		imageStyles: {
			type: Object,
			default() {
				return {
					width: 'auto',
					height: 'auto'
				}
			}
		},
		readonly: {
			type: Boolean,
			default: false
		},
		returnType: {
			type: String,
			default: 'array'
		},
		sizeType: {
			type: Array,
			default() {
				return ['original', 'compressed']
			}
		},
		sourceType: {
			type: Array,
			default() {
				return ['album', 'camera']
			}
		},
		provider: {
			type: String,
			default: '' // 默认上传到 unicloud 内置存储 extStorage 扩展存储
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			files: [],
			localValue: []
		}
	},
	watch: {
		value: {
			handler(newVal, oldVal) {
				this.setValue(newVal, oldVal)
			},
			immediate: true
		},
		modelValue: {
			handler(newVal, oldVal) {
				this.setValue(newVal, oldVal)
			},
			immediate: true
		},
	},
	computed: {
		filesList() {
			let files = []
			this.files.forEach(v => {
				files.push(v)
			})
			return files
		},
		showType() {
			if (this.fileMediatype === 'image') {
				return this.mode
			}
			return 'list'
		},
		limitLength() {
			if (this.returnType === 'object') {
				return 1
			}
			if (!this.limit) {
				return 1
			}
			if (this.limit >= 9) {
				return 9
			}
			return this.limit
		}
	},
	created() {
		// TODO 兼容不开通服务空间的情况
		if (!(uniCloud.config && uniCloud.config.provider)) {
			this.noSpace = true
			uniCloud.chooseAndUploadFile = chooseAndUploadFile
		}
		this.form = this.getForm('uniForms')
		this.formItem = this.getForm('uniFormsItem')
		if (this.form && this.formItem) {
			if (this.formItem.name) {
				this.rename = this.formItem.name
				this.form.inputChildrens.push(this)
			}
		}
	},
	methods: {
		/**
		 * 公开用户使用，清空文件
		 * @param {Object} index
		 */
		clearFiles(index) {
			if (index !== 0 && !index) {
				this.files = []
				this.$nextTick(() => {
					this.setEmit()
				})
			} else {
				this.files.splice(index, 1)
			}
			this.$nextTick(() => {
				this.setEmit()
			})
		},
		/**
		 * 公开用户使用，继续上传
		 */
		upload() {
			let files = []
			this.files.forEach((v, index) => {
				if (v.status === 'ready' || v.status === 'error') {
					files.push(Object.assign({}, v))
				}
			})
			return this.uploadFiles(files)
		},
		async setValue(newVal, oldVal) {
			const newData = async (v) => {
				const reg = /cloud:\/\/([\w.]+\/?)\S*/
				let url = ''
				if (v.fileID) {
					url = v.fileID
				} else {
					url = v.url
				}
				if (reg.test(url)) {
					v.fileID = url
					v.url = await this.getTempFileURL(url)
				}
				if (v.url) v.path = v.url
				return v
			}
			if (this.returnType === 'object') {
				if (newVal) {
					await newData(newVal)
				} else {
					newVal = {}
				}
			} else {
				if (!newVal) newVal = []
				for (let i = 0; i < newVal.length; i++) {
					let v = newVal[i]
					await newData(v)
				}
			}
			this.localValue = newVal
			if (this.form && this.formItem && !this.is_reset) {
				this.is_reset = false
				this.formItem.setValue(this.localValue)
			}
			let filesData = Object.keys(newVal).length > 0 ? newVal : [];
			this.files = [].concat(filesData)
		},

		/**
		 * 选择文件
		 */
		choose() {
			if (this.disabled) return
			if (this.files.length >= Number(this.limitLength) && this.showType !== 'grid' && this.returnType ===
				'array') {
				uni.showToast({
					title: `您最多选择 ${this.limitLength} 个文件`,
					icon: 'none'
				})
				return
			}
			this.chooseFiles()
		},

		/**
		 * 选择文件并上传
		 */
		chooseFiles() {
			const _extname = get_extname(this.fileExtname)
			// 获取后缀
			uniCloud
				.chooseAndUploadFile({
					type: this.fileMediatype,
					compressed: false,
					sizeType: this.sizeType,
					sourceType: this.sourceType,
					// TODO 如果为空，video 有问题
					extension: _extname.length > 0 ? _extname : undefined,
					count: this.limitLength - this.files.length, //默认9
					onChooseFile: this.chooseFileCallback,
					onUploadProgress: progressEvent => {
						this.setProgress(progressEvent, progressEvent.index)
					}
				})
				.then(result => {
					this.setSuccessAndError(result.tempFiles)
				})
				.catch(err => {
					console.log('选择失败', err)
				})
		},

		/**
		 * 选择文件回调
		 * @param {Object} res
		 */
		async chooseFileCallback(res) {
			const _extname = get_extname(this.fileExtname)
			const is_one = (Number(this.limitLength) === 1 &&
				this.disablePreview &&
				!this.disabled) ||
				this.returnType === 'object'
			// 如果这有一个文件 ，需要清空本地缓存数据
			if (is_one) {
				this.files = []
			}

			let {
				filePaths,
				files
			} = get_files_and_is_max(res, _extname)
			if (!(_extname && _extname.length > 0)) {
				filePaths = res.tempFilePaths
				files = res.tempFiles
			}

			let currentData = []
			for (let i = 0; i < files.length; i++) {
				if (this.limitLength - this.files.length <= 0) break
				files[i].uuid = Date.now()
				let filedata = await get_file_data(files[i], this.fileMediatype)
				filedata.progress = 0
				filedata.status = 'ready'
				this.files.push(filedata)
				currentData.push({
					...filedata,
					file: files[i]
				})
			}
			this.$emit('select', {
				tempFiles: currentData,
				tempFilePaths: filePaths
			})
			res.tempFiles = files
			// 停止自动上传
			if (!this.autoUpload || this.noSpace) {
				res.tempFiles = []
			}
			res.tempFiles.forEach((fileItem, index) => {
				this.provider && (fileItem.provider = this.provider);
				const fileNameSplit = fileItem.name.split('.')
				const ext = fileNameSplit.pop()
				const fileName = fileNameSplit.join('.').replace(/[\s\/\?<>\\:\*\|":]/g, '_')
				fileItem.cloudPath = fileName + '_' + Date.now() + '_' + index + '.' + ext
			})
		},

		/**
		 * 批传
		 * @param {Object} e
		 */
		uploadFiles(files) {
			files = [].concat(files)
			return uploadCloudFiles.call(this, files, 5, res => {
				this.setProgress(res, res.index, true)
			})
				.then(result => {
					this.setSuccessAndError(result)
					return result;
				})
				.catch(err => {
					console.log(err)
				})
		},

		/**
		 * 成功或失败
		 */
		async setSuccessAndError(res, fn) {
			let successData = []
			let errorData = []
			let tempFilePath = []
			let errorTempFilePath = []
			for (let i = 0; i < res.length; i++) {
				const item = res[i]
				const index = item.uuid ? this.files.findIndex(p => p.uuid === item.uuid) : item.index

				if (index === -1 || !this.files) break
				if (item.errMsg === 'request:fail') {
					this.files[index].url = item.path
					this.files[index].thumb = item.thumb
					this.files[index].status = 'error'
					this.files[index].errMsg = item.errMsg
					// this.files[index].progress = -1
					errorData.push(this.files[index])
					errorTempFilePath.push(this.files[index].url)
				} else {
					this.files[index].errMsg = ''
					this.files[index].fileID = item.thumb || item.url
					const reg = /cloud:\/\/([\w.]+\/?)\S*/
					if (reg.test(item.thumb || item.url)) {
						this.files[index].url = await this.getTempFileURL(item.thumb || item.url)
					} else {
						this.files[index].url = item.thumb || item.url
					}

					this.files[index].status = 'success'
					this.files[index].progress += 1
					successData.push(this.files[index])
					tempFilePath.push(this.files[index].fileID)
				}
			}

			if (successData.length > 0) {
				this.setEmit()
				// 状态改变返回
				this.$emit('success', {
					tempFiles: this.backObject(successData),
					tempFilePaths: tempFilePath
				})
			}

			if (errorData.length > 0) {
				this.$emit('fail', {
					tempFiles: this.backObject(errorData),
					tempFilePaths: errorTempFilePath
				})
			}
		},

		/**
		 * 获取进度
		 * @param {Object} progressEvent
		 * @param {Object} index
		 * @param {Object} type
		 */
		setProgress(progressEvent, index, type) {
			const fileLenth = this.files.length
			const percentNum = (index / fileLenth) * 100
			const percentCompleted = Math.round((progressEvent.loaded * 100) / progressEvent.total)
			let idx = index
			if (!type) {
				idx = this.files.findIndex(p => p.uuid === progressEvent.tempFile.uuid)
			}
			if (idx === -1 || !this.files[idx]) return
			// fix by mehaotian 100 就会消失，-1 是为了让进度条消失
			this.files[idx].progress = percentCompleted - 1
			// 上传中
			this.$emit('progress', {
				index: idx,
				progress: parseInt(percentCompleted),
				tempFile: this.files[idx]
			})
		},

		/**
		 * 删除文件
		 * @param {Object} index
		 */
		delFile(index) {
			this.$emit('delete', {
				index,
				tempFile: this.files[index],
				tempFilePath: this.files[index].url
			})
			this.files.splice(index, 1)
			this.$nextTick(() => {
				this.setEmit()
			})
		},

		/**
		 * 获取文件名和后缀
		 * @param {Object} name
		 */
		getFileExt(name) {
			const last_len = name.lastIndexOf('.')
			const len = name.length
			return {
				name: name.substring(0, last_len),
				ext: name.substring(last_len + 1, len)
			}
		},

		/**
		 * 处理返回事件
		 */
		setEmit() {
			let data = []
			if (this.returnType === 'object') {
				data = this.backObject(this.files)[0]
				this.localValue = data ? data : null
			} else {
				data = this.backObject(this.files)
				if (!this.localValue) {
					this.localValue = []
				}
				this.localValue = [...data]
			}
			// #ifdef VUE3
			this.$emit('update:modelValue', this.localValue)
			// #endif
			// #ifndef VUE3
			this.$emit('input', this.localValue)
			// #endif
		},

		/**
		 * 处理返回参数
		 * @param {Object} files
		 */
		backObject(files) {
			let newFilesData = []
			files.forEach(v => {
				newFilesData.push({
					extname: v.extname,
					fileType: v.fileType,
					image: v.image,
					name: v.name,
					path: v.path,
					size: v.size,
					fileID: v.fileID,
					url: v.url,
					// 修改删除一个文件后不能再上传的bug, #694
					uuid: v.uuid,
					status: v.status,
					cloudPath: v.cloudPath
				})
			})
			return newFilesData
		},
		async getTempFileURL(fileList) {
			fileList = {
				fileList: [].concat(fileList)
			}
			const urls = await uniCloud.getTempFileURL(fileList)
			return urls.fileList[0].tempFileURL || ''
		},
		/**
		 * 获取父元素实例
		 */
		getForm(name = 'uniForms') {
			let parent = this.$parent;
			let parentName = parent.$options.name;
			while (parentName !== name) {
				parent = parent.$parent;
				if (!parent) return false;
				parentName = parent.$options.name;
			}
			return parent;
		}
	}
}
</script>

<style lang="scss">
@import './upload.scss';
</style>