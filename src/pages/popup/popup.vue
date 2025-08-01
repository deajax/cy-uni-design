<template>
	<view class="popup">
		<cy-button variant="outline" block @click="showTop">
			顶部弹出
		</cy-button>

		<cy-button variant="outline" block @click="showBottom">
			底部弹出
		</cy-button>

		<cy-button variant="outline" block @click="showLeft">
			左侧弹出
		</cy-button>

		<cy-button variant="outline" block @click="showRight">
			右侧弹出
		</cy-button>

		<cy-button variant="outline" block @click="$refs.center.open()">
			中间弹出
		</cy-button>

		<cy-popup ref="top" type="top">
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
		</cy-popup>

		<cy-popup ref="bottom" type="bottom" title="底部弹出" close-btn>
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
		</cy-popup>

		<cy-popup ref="left" type="left">
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
		</cy-popup>

		<cy-popup ref="right" type="right">
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
		</cy-popup>

		<cy-popup ref="center" type="center">
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;">123</view>
			<view style="padding: 16px;" @click="$refs.center.close()">close</view>
		</cy-popup>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
		}
	},
	computed: {},
	methods: {
		showTop() { this.$refs.top.open('top') },
		showBottom() { this.$refs.bottom.open('bottom') },
		showLeft() { this.$refs.left.open('left') },
		showRight() { this.$refs.right.open('right') },
		showCenter() { this.$refs.center.open('center') },
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

<style lang="scss">
.popup {
	padding: 16px;
	display: flex;
	flex-direction: column;
	row-gap: 8px;
}
</style>