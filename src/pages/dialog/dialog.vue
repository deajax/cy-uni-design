<template>
	<view class="dialog">
		<cy-button
				   theme="primary"
				   size="large"
				   variant="outline"
				   @click="show1 = !show1"
				   block>
			基础对话框
		</cy-button>
		<cy-dialog
				   :visible="show1"
				   title="对话框标题"
				   content="告知当前状态、信息和解决方法，等内容。描述文案尽可能控制在三行内"
				   :confirm-btn="{ content: '知道了', variant: 'base' }"
				   @confirm="show1 = false" />


		<cy-button
				   theme="primary"
				   size="large"
				   variant="outline"
				   @click="show2 = !show2"
				   block>
			确认类对话框
		</cy-button>
		<cy-dialog
				   :visible="show2"
				   title="对话框标题"
				   content="告知当前状态、信息和解决方法，等内容。描述文案尽可能控制在三行内"
				   confirm-btn
				   cancel-btn
				   @confirm="show2 = false" />


		<cy-button
				   theme="primary"
				   size="large"
				   variant="outline"
				   @click="show3 = !show3"
				   block>
			垂直基础按钮
		</cy-button>
		<cy-dialog
				   :visible="show3"
				   title="对话框标题"
				   content="告知当前状态、信息和解决方法，等内容。描述文案尽可能控制在三行内"
				   confirm-btn
				   cancel-btn
				   button-layout="vertical"
				   @confirm="show3 = false" />
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			show1: false,
			show2: false,
			show3: false,
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
.dialog {
	padding: 16px;
	display: flex;
	flex-direction: column;
	row-gap: 8px;
}
</style>