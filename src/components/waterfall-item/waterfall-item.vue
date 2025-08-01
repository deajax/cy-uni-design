<template>
	<view :class="['cy-waterfall-item', customClass]" @tap="handleTap">
		<slot />
	</view>
</template>

<script>
export default {
	name: 'waterfall-item',
	externalClasses: ['custom-class'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		url: {
			type: String,
			default: ''
		},
		jumpType: {
			type: String,
			default: 'navigate-to'
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		}
	},
	data() {
		return {};
	},
	computed: {},
	methods: {
		handleTap(event) {
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
		}
	},
	watch: {},

	// 组件周期函数--监听组件挂载完毕
	mounted() {},
	// 组件周期函数--监听组件数据更新之前
	beforeUpdate() {},
	// 组件周期函数--监听组件数据更新之后
	updated() {},
	// 组件周期函数--监听组件激活(显示)
	activated() {},
	// 组件周期函数--监听组件停用(隐藏)
	deactivated() {},
	// 组件周期函数--监听组件销毁之前
	beforeDestroy() {}
};
</script>

<style lang="scss">
@import './waterfall-item.scss';
</style>
