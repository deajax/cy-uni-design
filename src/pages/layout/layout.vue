<template>
	<view class="layout">
		<view class="title">基础</view>
		<view class="example">
			<cy-row>
				<cy-col span="8">
					<view class="dark">col-8</view>
				</cy-col>
				<cy-col span="8">
					<view class="dark">col-8</view>
				</cy-col>
				<cy-col span="8">
					<view class="dark">col-8</view>
				</cy-col>
			</cy-row>

			<cy-row>
				<cy-col span="4">
					<view class="dark">col-4</view>
				</cy-col>
				<cy-col span="16" offset="4">
					<view class="dark">col-16 col-offset-4</view>
				</cy-col>
			</cy-row>

			<cy-row>
				<cy-col offset="12" span="12">
					<view class="dark">col-12 col-offset-12</view>
				</cy-col>
			</cy-row>
		</view>

		<view class="title">增加间距</view>
		<view class="example">
			<cy-row gutter="16">
				<cy-col span="8">
					<view class="dark">col-8</view>
				</cy-col>
				<cy-col span="8">
					<view class="dark">col-8</view>
				</cy-col>
				<cy-col span="8">
					<view class="dark">col-8</view>
				</cy-col>
			</cy-row>
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
	// 页面周期函数--监听页面显示(nocy-nvue)
	onShow() { },
	// 页面周期函数--监听页面隐藏
	onHide() { },
	// 页面周期函数--监听页面卸载
	onUnload() { },
	// 页面处理函数--监听用户下拉动作
	// onPullDownRefresh() { uni.stopPullDownRefresh(); },
	// 页面处理函数--监听用户上拉触底
	// onReachBottom() {},
	// 页面处理函数--监听页面滚动(nocy-nvue)
	// onPageScroll(event) {},
	// 页面处理函数--用户点击右上角分享
	// onShareAppMessage(options) {},
} 
</script>

<style lang="scss">
.example {
	padding: 0 16px;

	.dark {
		padding: 8px;
		background: cornflowerblue;
	}
}
</style>