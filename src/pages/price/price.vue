<template>
	<view class="price">
		<view class="title">不同主题</view>
		<view class="example">
			<cy-price v-model="price" />
			<cy-price v-model="price" theme="primary" />
			<cy-price v-model="price" theme="warning" />
			<cy-price v-model="price" theme="danger" />
			<cy-price v-model="price" theme="success" />
		</view>

		<view class="title">不同尺寸</view>
		<view class="example">
			<cy-price v-model="price" size="small" />
			<cy-price v-model="price" size="medium" />
			<cy-price v-model="price" size="large" />
			<cy-price v-model="price" size="extra-large" />
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			price: '49.98'
		}
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
	display: flex;
	gap: 12px;
}
</style>