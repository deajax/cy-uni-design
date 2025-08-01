<template>
	<view class="search">
		<view class="example">
			<cy-search v-model="search" placeholder="请输入搜索内容"></cy-search>
		</view>

		<view class="example">
			<cy-search v-model="search" placeholder="请输入搜索内容" shape="round"></cy-search>
		</view>

		<view class="example">
			<cy-search v-model="search" placeholder="请输入搜索内容" action="取消" @action-click="onActionClick"></cy-search>
		</view>

		<view class="example">
			<cy-search v-model="search" placeholder="禁用输入框" shape="round" disabled></cy-search>
		</view>

		<view class="example">
			<cy-search>
				<template #input>
					自定义内容
				</template>
			</cy-search>
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			search: ""
		}
	},
	computed: {},
	methods: {
		onActionClick(e) {
			console.log('您点击了取消按钮', e);
		}
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
page {
	background: #f5f5f5;
}
</style>