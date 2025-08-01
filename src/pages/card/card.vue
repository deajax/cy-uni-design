<template>
	<view class="card">
		<view class="example">
			<cy-card title="标题" extra="额外内容" theme="card">
				内容
			</cy-card>
		</view>

		<view class="example">
			<cy-card title="标题" extra="额外内容">
				内容
			</cy-card>
		</view>

		<view class="example">
			<cy-card title="标题" extra="额外内容">
				<view class="">
					内容
				</view>
				<view class="flex" slot="action">
					<cy-icon name="settings-4-line"></cy-icon>
					<cy-icon name="edit-line"></cy-icon>
					<cy-icon name="more-line"></cy-icon>
				</view>
			</cy-card>
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

.card {
	padding-top: 32rpx;
}
</style>