<template>
	<view class="navbar">
		<view class="example">
			<cy-navbar title="标题文字标题文字标题文字" />
		</view>

		<view class="title">带返回按钮</view>
		<view class="example">
			<cy-navbar title="标题文字" left-arrow :fixed="false" />
		</view>

		<view class="title">自定义</view>
		<view class="example">
			<cy-navbar :fixed="false">
				<view class="" slot="left">
					left
				</view>
				<view class="" slot="title">
					自定义插槽
				</view>
			</cy-navbar>
		</view>

		<view class="title">自定义颜色</view>
		<view class="example">
			<cy-navbar title="标题文字" left-arrow custom-class="custom-navbar" :fixed="false" />
			<view class="code">
				<view>.custom-navbar {
					--cy-navbar-color: #fff;
					--cy-navbar-bg-color: #0052d9;
					}</view>
			</view>
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
page {
	background: #f5f5f5;
}

.custom-navbar {
	--cy-navbar-color: #fff;
	--cy-navbar-bg-color: #0052d9;
}
</style>