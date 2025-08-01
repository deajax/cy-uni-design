<template>
	<view class="stepper">
		<view class="title">基础步进器</view>
		<view class="example">
			<cy-stepper />
		</view>

		<view class="title">最大最小状态</view>
		<view class="example">
			<cy-stepper default-value="0" />
			<cy-stepper default-value="5" min="5" />
			<cy-stepper default-value="99" min="5" max="99" />
		</view>

		<view class="title">禁用状态</view>
		<view class="example">
			<cy-stepper theme="filled" disabled />
			<cy-stepper theme="outline" disabled />
			<cy-stepper disabled />
		</view>

		<view class="title">步进器样式</view>
		<view class="example">
			<cy-stepper theme="filled" />
			<cy-stepper theme="outline" />
			<cy-stepper />
		</view>

		<view class="title">步进器尺寸</view>
		<view class="example">
			<cy-stepper theme="filled" size="large" />
			<cy-stepper theme="filled" />
			<cy-stepper theme="filled" size="small" />
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {}
	},
	computed: {},
	methods: {},
	watch: {},

	// 页面周期函数--监听页面加载
	onLoad() { },
	// 页面周期函数--监听页面初次渲染完成
	onReady() { },
	// 页面周期函数--监听页面显示(not-nvue)
	onShow() { },
	// 页面周期函数--监听页面隐藏
	onHide() { },
	// 页面周期函数--监听页面卸载
	onUnload() { },
	// 页面处理函数--监听用户下拉动作
	// onPullDownRefresh() { uni.stopPullDownRefresh(); },
	// 页面处理函数--监听用户上拉触底
	// onReachBottom() {},
	// 页面处理函数--监听页面滚动(not-nvue)
	// onPageScroll(event) {},
	// 页面处理函数--用户点击右上角分享
	// onShareAppMessage(options) {},
} 
</script>

<style lang="scss">
.example {
	display: flex;
	padding: 0 16px;
	gap: 16px;
}
</style>