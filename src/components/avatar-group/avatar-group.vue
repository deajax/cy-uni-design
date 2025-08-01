<template>
	<view :style="[customStyle]"
		  :class="['cy-avatar-group', `cy-avatar-group-offset-${cascading}-${size}`, customClass]">
		<slot />
		<!-- 自定义折叠元素 -->
		<view class="cy__collapse--slot">
			<slot name="collapse-avatar" />
		</view>
		<!-- 默认折叠元素 -->
		<view class="cy__collapse--default" v-if="max">
			<cy-avatar
					   :custom-class-image="`cy-avatar--border cy-avatar--${size} ` + customClassImage"
					   :custom-class-content="'cy-class-content ' + customClassContent"
					   :size="size"
					   :icon="collapseAvatar ? '' : 'user-add-line'">{{ collapseAvatar }}</cy-avatar>
		</view>
	</view>
</template>

<script>
export default {
	name: "avatar-group",
	externalClasses: ['custom-class', 'custom-class-image', 'custom-class-content'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		/** 图片之间的层叠关系，可选值：左侧图片在上和右侧图片在上 */
		cascading: {
			type: String,
			default: 'left-up',
		},
		/** 头像数量超出时，会出现一个头像折叠元素。该元素内容可自定义。默认为 `+N`。示例：`+5`，`...`, `更多` */
		collapseAvatar: {
			type: String,
			default: ''
		},
		/** 组件类名，用于设置组件外层元素类名 */
		externalClasses: {
			type: Array,
			default: ''
		},
		/** 能够同时显示的最多头像数量 */
		max: {
			type: [Number, String],
			default: ''
		},
		/** 尺寸，示例值：small/medium/large/24px/38px 等。优先级低于 Avatar.size */
		size: {
			type: String,
			default: 'medium',
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassImage: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
		// externalStyles
		customStyle: {
			type: [String, Object],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {
	},
	methods: {},
	watch: {},

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

<style lang="scss">
@import './avatar-group.scss';
</style>