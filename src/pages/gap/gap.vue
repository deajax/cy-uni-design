<template>
	<view class="gap">
		<view class="title">列间隔</view>
		<view class="example">
			<cy-gap gutter="8">
				<cy-tag variant="light">标签文字</cy-tag>
				<cy-tag variant="outline">标签文字</cy-tag>
				<cy-tag variant="outline">标签文字</cy-tag>
			</cy-gap>
		</view>

		<view class="title">行间隔和列间隔</view>
		<view class="example">
			<cy-gap :gutter="[8, 16]">
				<cy-tag variant="outline" v-for="i in 12" :key="i">标签文字</cy-tag>
			</cy-gap>
		</view>

		<view class="title">纵向布局</view>
		<view class="example">
			<cy-gap layout="vertical" :gutter="[0, 8]">
				<cy-button variant="outline" block>填充按钮</cy-button>
				<cy-button variant="outline" block>填充按钮</cy-button>
				<cy-button variant="outline" block>填充按钮</cy-button>
			</cy-gap>
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
	padding: 0 16px;
}
</style>