<template>
	<view class="fab">
		<cy-fab :scrollTop="scrollTop" backtop>
			solt
		</cy-fab>
		<view>
			<view v-for="i in 300" :key="i">{{ i }}</view>
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			scrollTop: 0
		}
	},
	computed: {},
	methods: {
		onPageScroll(e) {
			this.scrollTop = e.scrollTop;
		},
	},
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

<style lang="scss"></style>