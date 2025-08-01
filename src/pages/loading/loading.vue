<template>
	<view class="loading">
		<view class="title">纯图标</view>
		<view class="example">
			<cy-loading></cy-loading>
		</view>

		<view class="title">图标加文字横向</view>
		<view class="example">
			<cy-loading text="加载中..."></cy-loading>
		</view>

		<view class="title">图标加文字竖向</view>
		<view class="example">
			<cy-loading text="加载中" layout="vertical"></cy-loading>
		</view>

		<view class="title">纯文字</view>
		<view class="example">
			<cy-loading text="加载中..." :indicator="false"></cy-loading>
		</view>

		<view class="title">组件颜色</view>
		<view class="example">
			<cy-loading text="加载中..." color="blue"></cy-loading>
			<cy-loading text="加载中..." color="red"></cy-loading>
			<cy-loading text="加载中..." color="gray"></cy-loading>
		</view>

		<view class="title">配合Empty组件制作页面加载效果</view>
		<view class="example">
			<cy-empty description="数据加载中">
				<template #icon>
					<cy-loading />
				</template>
			</cy-empty>
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