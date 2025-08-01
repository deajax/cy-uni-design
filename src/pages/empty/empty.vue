<template>
	<view class="empty">
		<view class="title">状态类型</view>
		<view class="example">
			<cy-empty image="default" description="默认状态" />
			<cy-empty image="item" description="暂无商品" />
			<cy-empty image="search" description="没有找到你想要的结果" />
			<cy-empty image="network" description="网络无法连接" />
			<cy-empty image="list" description="暂无订单记录" />
		</view>

		<view class="title">自定义图标</view>
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
</style>