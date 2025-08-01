<template>
	<view class="sticky">
		<view class="title">基础吸顶</view>
		<cy-sticky>
			<cy-button>吸顶</cy-button>
		</cy-sticky>
		<view v-for="i in 20" :key="i" class="span">
			{{ i }}
		</view>

		<view class="title">吸顶距离</view>
		<cy-sticky :offset-top="100">
			<cy-button>吸顶距离</cy-button>
		</cy-sticky>
		<view v-for="i in 20" :key="i" class="span">
			{{ i }}
		</view>

		<view class="title">框内吸顶</view>
		<view class="example" style="height: 300px; border: 1px solid #000; margin: 0 40px;">
			<cy-sticky>
				<cy-button>吸顶</cy-button>
			</cy-sticky>
		</view>
		<view v-for="i in 50" :key="i" class="span">
			{{ i }}
		</view>
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
#container {
	height: 250px;
	background-color: #E0E0E0;
}
</style>