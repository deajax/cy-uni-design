<template>
	<view :class="['cy-waterfall', customClass]" :style="{ columns: columns, gap: gap + 'rpx' }">
		<slot />
	</view>
</template>

<script>
export default {
	name: "waterfall",
	externalClasses: ['custom-class'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		columns: {
			type: [String, Number],
			default: 2
		},
		gap: {
			type: [String, Number],
			default: 24
		},
		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {},
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