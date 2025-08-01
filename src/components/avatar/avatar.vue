<template>
	<view :class="['cy-avatar__wrapper', customClass]" :style="[style, customStyle]">
		<cy-badge
				  :color="badgeProps.color || ''"
				  :content="badgeProps.content || ''"
				  :count="badgeProps.count || 0"
				  :dot="badgeProps.dot || false"
				  :max-count="badgeProps.maxCount || 99"
				  :offset="badgeProps.offset || []"
				  :shape="badgeProps.shape || 'circle'"
				  :show-zero="badgeProps.showZero || false"
				  :size="badgeProps.size || 'medium'"
				  :custom-class="badgeProps.customClass"
				  :custom-class-content="badgeProps.customClassContent"
				  :custom-class-count="badgeProps.customClassCount">
			<view
				  :class="['cy-avatar', `cy-avatar--${size}`, `cy-avatar--${shape}`, bordered ? 'cy-avatar--border' : '']"
				  :style="[getSize]">
				<image
					   v-if="image"
					   :src="image"
					   :class="['cy-avatar__image', customClassImage, imageProps && imageProps.shape || 'cy-avatar__round']"
					   :style="imageProps && imageProps.style || ''"
					   :mode="imageProps && imageProps.mode || 'aspectFill'" />
				<cy-icon v-else-if="icon || icon.name" custom-class="cy-avatar__icon" :name="icon || icon.name" />
				<view v-else :class="['cy-avatar__text', customClassContent]">
					<slot />
				</view>
			</view>
		</cy-badge>
	</view>
</template>

<script>
export default {
	name: "avatar",
	externalClasses: ['custom-class', 'custom-class-label', 'custom-class-wrapper', 'custom-class-indicator'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		/** 头像替换文本，仅当图片加载失败时有效 */
		alt: {
			type: String,
			default: '',
		},
		/** 头像右上角提示信息，继承 Badge 组件的全部特性。如：小红点，或者数字 */
		badgeProps: {
			type: Object,
		},
		/** 是否显示外边框 */
		bordered: {
			type: Boolean,
			default: false,
		},
		/** 组件类名，用于设置组件外层元素类名 */
		externalClasses: {
			type: Array,
		},
		/** 加载失败时隐藏图片 */
		hideOnLoadFailed: {
			type: Boolean,
			default: false,
		},
		/** 图标。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon`。 */
		icon: {
			type: null,
			default: '',
		},
		/** 图片地址 */
		image: {
			type: String,
			default: '',
		},
		/** 透传至 Image 组件 */
		imageProps: {
			type: Object,
		},
		/** 形状 */
		shape: {
			type: String,
			default: 'circle',
		},
		/** 尺寸，示例值：small/medium/large/24px/38px 等 */
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
		style() { },
		getSize() { },
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
@import './avatar.scss';
</style>