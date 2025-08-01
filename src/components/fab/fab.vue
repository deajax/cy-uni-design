<template>
	<view :class="['cy-fab', customClass]" :style="customStyle">
		<slot />
		<cy-button v-if="backtop && show"
				   :custom-class="'cy-fab--backtop ' + customClassBacktop"
				   icon="rocket-line"
				   shape="circle"
				   @click="toTop" />
	</view>
</template>

<script>
export default {
	name: "fab",
	externalClasses: ['custom-class', 'custom-class-backtop'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		scrollTop: {
			type: Number,
			default: 0
		},
		backtop: Boolean,
		customStyle: {
			type: [Object, Array, String],
			default: 'right: 16px; bottom: 48px;'
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassBacktop: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			top: 300,
		}
	},
	computed: {
		show() {
			let top
			// 如果是rpx，转为px
			if (/rpx$/.test(this.top)) {
				top = uni.rpx2px(parseInt(this.top))
			} else {
				top = parseInt(this.top)
			}
			return this.scrollTop > top
		},
	},
	methods: {
		toTop(event) {
			this.$emit('to-top', event);
			uni.pageScrollTo({
				scrollTop: 0,
				duration: 300
			});
		}
	},
	watch: {},

	// 组件周期函数--监听组件挂载完毕
	onReady() { },
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
@import './fab.scss';
</style>