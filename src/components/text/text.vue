<template>
	<view :class="['cy-text', customClass, setClass, `cy-text--${theme}`, `cy-text--${size}`]"
		  :hover-class="hover && !disabled && 'cy-text--hover'"
		  @click="handleTap">
		<view class="cy-text__prefix-icon">
			<slot name="prefix-icon" />
			<cy-icon v-if="prefixIcon"
					 :name="prefixIcon.name || prefixIcon"
					 :size="prefixIcon.size || ''"
					 :color="prefixIcon.color || ''"
					 :custom-class="'cy-text-prefix-icon ' + customClassPrefixIcon" />
			<image
				v-if="image"
				:src="image.src || image"
				:mode="image.mode || 'aspectFit'"
				:style="{ width: image.width || '32rpx', height: image.height || '32rpx', display: 'block' }"
			/>
		</view>
		<view class="cy-text__content" :class="customClassContent">
			<template v-if="content">{{ content }}</template>
			<slot name="content" />
			<slot />
		</view>
		<view class="cy-text__suffix-icon">
			<slot name="suffix-icon" />
			<cy-icon v-if="suffixIcon"
					 :name="suffixIcon.name || suffixIcon"
					 :size="suffixIcon.size || ''"
					 :color="suffixIcon.color || ''"
					 :custom-class="'cy-text-suffix-icon ' + customClassSuffixIcon" />
		</view>
	</view>
</template>

<script>
export default {
	name: "Text",
	externalClasses: ['custom-class', 'custom-class-prefix-icon', 'custom-class-content', 'custom-class-suffix-icon'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		content: null,
		prefixIcon: [String, Object],
		suffixIcon: [String, Object],
		disabled: Boolean,
		hover: Boolean,
		underline: Boolean,
		size: {
			type: String,
			default: 'medium'
		},
		theme: {
			type: String,
			default: 'default'
		},
		url: {
			type: String
		},
		image: {
			type: [String, Object]
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
		customClassPrefixIcon: {
			type: [String, Array],
			default: ''
		},
		customClassSuffixIcon: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {
		setClass() {
			if (this.underline) {
				return 'cy-text--underline'
			}
			if (this.disabled) {
				return 'cy-text--disabled'
			}
		},
	},
	methods: {
		handleTap(event) {
			if (this.disabled) return;

			this.$emit('click', event);
			this.stop && this.preventEvent(event);
			if (!this.url) return;
			if (this.jumpType == 'navigateTo') {
				uni.navigateTo({
					url: this.url
				});
			} else if (this.jumpType == 'switchTab') {
				uni.switchTab({
					url: this.url
				});
			} else if (this.jumpType == 'reLaunch') {
				uni.reLaunch({
					url: this.url
				});
			} else if (this.jumpType == 'redirectTo') {
				uni.redirectTo({
					url: this.url
				});
			} else {
				uni.navigateTo({
					url: this.url
				});
			}
		},
	},
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
@import './text.scss';
</style>