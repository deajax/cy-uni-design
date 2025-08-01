<template>
	<view :class="['cy-upload__grid ' + customClassGrid]">
		<cy-row gutter="8" gap="8">
			<cy-col span="6" v-for="(item, index) in filesList" :key="index">
				<view class="cy-upload__grid--item">
					<view class="cy-upload__wrapper">
						<image :class="['cy-upload__thumbnail', customClassThumbnail]" :src="item.url" mode="aspectFill"
							   @click.stop="prviewImage(item, index)"></image>
						<view v-if="delIcon && !readonly" :class="['cy-upload__close-btn', customClassClose]"
							  @click.stop="delFile(index)">
							<cy-icon name="close-line" size="32" color="#fff" />
						</view>
						<view v-if="item.status === 'uploading' || item.status === 'failed'"
							  :class="['cy-upload__progress-mask', customClassMask]">
							<view v-if="(item.progress && item.progress !== 100) || item.progress === 0"
								  class="file-picker__progress">
								<cy-loading :custom-class="['cy-upload__progress-loading ' + customClassLoading]"
											:text="item.progress === -1 ? '上传中...' : item.progress + '%'"
											layout="vertical" />
							</view>
							<view v-if="item.errMsg" class="cy-upload__progress-mask--inner"
								  @click.stop="uploadFiles(item, index)">
								<cy-icon :custom-class="['cy-upload__progress-icon ' + customClassIcon]"
										 name="refresh-line" />
								<text class="cy-upload__progress-text">重新上传</text>
							</view>
						</view>
					</view>
				</view>
			</cy-col>
			<cy-col span="6">
				<view v-if="filesList.length < limit && !readonly" class="cy-upload__grid--item">
					<view :class="['cy-upload__wrapper', customClassWrapper]" @click="choose">
						<view class="cy-upload__add-icon">
							<slot></slot>
						</view>
					</view>
				</view>
			</cy-col>
		</cy-row>
	</view>
</template>

<script>
export default {
	name: "upload-image",
	emits: ['uploadFiles', 'choose', 'delFile'],
	externalClasses: ['custom-class-grid', 'custom-class-wrapper', 'custom-class-thumbnail', 'custom-class-mask', 'custom-class-loading', 'custom-class-icon', 'custom-class-close'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		filesList: {
			type: Array,
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
		limit: {
			type: [Number, String],
			default: 9
		},
		imageStyles: {
			type: Object,
			default() {
				return {
					width: 'auto',
					height: 'auto',
					border: {}
				}
			}
		},
		delIcon: {
			type: Boolean,
			default: true
		},
		readonly: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClassGrid: {
			type: [String, Array],
			default: ''
		},
		customClassWrapper: {
			type: [String, Array],
			default: ''
		},
		customClassThumbnail: {
			type: [String, Array],
			default: ''
		},
		customClassMask: {
			type: [String, Array],
			default: ''
		},
		customClassLoading: {
			type: [String, Array],
			default: ''
		},
		customClassIcon: {
			type: [String, Array],
			default: ''
		},
		customClassClose: {
			type: [String, Array],
			default: ''
		},
	},
	computed: {},
	methods: {
		uploadFiles(item, index) {
			this.$emit("uploadFiles", item)
		},
		choose() {
			this.$emit("choose")
		},
		delFile(index) {
			this.$emit('delFile', index)
		},
		prviewImage(img, index) {
			let urls = []
			if (Number(this.limit) === 1 && this.disablePreview && !this.disabled) {
				this.$emit("choose")
			}
			if (this.disablePreview) return
			this.filesList.forEach(i => {
				urls.push(i.url)
			})

			uni.previewImage({
				urls: urls,
				current: index
			});
		},
		value2px(value) {
			if (typeof value === 'number') {
				value += 'px'
			} else {
				if (value.indexOf('%') === -1) {
					value = value.indexOf('px') !== -1 ? value : value + 'px'
				}
			}
			return value
		}
	}
} 
</script>