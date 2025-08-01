<template>
	<view class="divider">
		<view class="title">基础分割符</view>
		<view class="example">
			<cy-divider />
		</view>

		<view class="title">带文字水平分割线</view>
		<view class="example">
			<cy-divider content="文字信息" align="left" />
			<cy-divider content="文字信息" />
			<cy-divider content="文字信息" align="right" />
		</view>

		<view class="title">垂直分割线</view>
		<view class="example flex">
			<text>文字信息</text>
			<cy-divider layout="vertical" />
			<text>文字信息</text>
			<cy-divider layout="vertical" />
			<text>文字信息</text>
		</view>

		<view class="title">虚线样式</view>
		<view class="example">
			<cy-divider dashed />
			<cy-divider dashed content="文字信息" align="left" />
			<cy-divider dashed content="文字信息" />
			<cy-divider dashed content="文字信息" align="right" />
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