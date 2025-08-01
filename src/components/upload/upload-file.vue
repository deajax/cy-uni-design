<template>
	<view :class="['cy-upload__files', customClassFiles]">
		<view v-if="!readonly" :class="['cy-upload__files-action', customClassAction]" @click="choose">
			<slot></slot>
		</view>
		<view :class="['cy-upload__files--list', customClassList]" v-if="list.length > 0">
			<cy-cell :title="item.name" v-for="(item, index) in list" :key="index">
				<template #left-icon>
					<cy-icon v-if="item.status === 'error'" name="close-line" :size="40" color="#ef4444" />
				</template>
				<template #right-icon>
					<view v-if="delIcon && !readonly" class="cy-upload__files--close-btn" @click="delFile(index)">
						<cy-divider layout="vertical" />
						<cy-icon name="delete-bin-line" :size="40" color="rgba(0, 0, 0, 0.4)" />
					</view>
				</template>
				<template #note>
					<view v-if="item.status === 'error'"
						  class="cy-upload__files--progress"
						  @click.stop="uploadFiles(item, index)">
						重新上传
					</view>
				</template>
			</cy-cell>
		</view>
	</view>
</template>

<script>
export default {
	name: "upload-file",
	emits: ['uploadFiles', 'choose', 'delFile'],
	externalClasses: ['custom-class-files', 'custom-class-action', 'custom-class-list'],
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
		delIcon: {
			type: Boolean,
			default: true
		},
		limit: {
			type: [Number, String],
			default: 9
		},
		showType: {
			type: String,
			default: ''
		},
		readonly: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClassFiles: {
			type: [String, Array],
			default: ''
		},
		customClassAction: {
			type: [String, Array],
			default: ''
		},
		customClassList: {
			type: [String, Array],
			default: ''
		},
	},
	computed: {
		list() {
			let files = []
			this.filesList.forEach(v => {
				files.push(v)
			})
			return files
		},
	},
	methods: {
		uploadFiles(item, index) {
			this.$emit("uploadFiles", {
				item,
				index
			})
		},
		choose() {
			this.$emit("choose")
		},
		delFile(index) {
			this.$emit('delFile', index)
		},
		value2px(value) {
			if (typeof value === 'number') {
				value += 'px'
			} else {
				value = value.indexOf('px') !== -1 ? value : value + 'px'
			}
			return value
		}
	},

	// 组件周期函数--监听组件挂载完毕
	mounted() { },
	// 组件周期函数--监听组件数据更新之前
	beforeUpdate() { },
	// 组件周期函数--监听组件数据更新之后
	updated() { },
	// 组件周期函数--监听组件激活(显示)
	activated() { },
	// 组件周期函数--监听组件停用(隐藏)
	deactivated() { },
	// 组件周期函数--监听组件销毁之前
	beforeDestroy() { },
} 
</script>