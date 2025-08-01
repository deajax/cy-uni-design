<template>
	<view class="waterfall">
		<cy-waterfall>
			<cy-waterfall-item v-for="i in 15" :key="i"
							   image="https://via.placeholder.com/180"
							   :title="i % 3 != 0 ? '商品标题' : '商品标题商品标题商品标题商品标题商品标题'"
							   description="描述信息"
							   price="2.00"
							   origin-price="3.00"
							   unit="盒350g">
				<view class="">slot</view>
				<view class="" slot="extra">extra</view>
			</cy-waterfall-item>
		</cy-waterfall>
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

.waterfall {
	padding: 16px;
}
</style>