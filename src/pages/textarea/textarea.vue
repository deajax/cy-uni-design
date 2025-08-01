<template>
	<view class="textarea">
		<view class="title">基础多行文本框</view>
		<view class="example">
			<cy-textarea placeholder="请输入文字" disable-default-padding />
		</view>

		<view class="title">带标题多行文本框</view>
		<view class="example">
			<cy-textarea label="标签文字" placeholder="请输入文字" disable-default-padding />
		</view>

		<view class="title">自动增高多行文本框</view>
		<view class="example">
			<cy-textarea
						 label="标签文字"
						 placeholder="请输入文字"
						 disable-default-padding
						 autosize
						 @line-change="onLineChange" />
		</view>

		<view class="title">设置最大字符个数</view>
		<view class="example">
			<cy-textarea
						 label="标签文字"
						 placeholder="设置最大字符个数"
						 maxlength="200"
						 disable-default-padding
						 indicator />
		</view>

		<view class="title">禁用多行文本框</view>
		<view class="example">
			<cy-textarea
						 label="标签文字"
						 placeholder="请输入文字"
						 value="不可编辑文字"
						 disable-default-padding
						 disabled />
		</view>

		<view class="title">标签外置输入框</view>
		<view class="textarea-example">
			<text class="textarea-example__label">标签文字</text>
			<cy-textarea
						 custom-class="external-class"
						 placeholder="请输入文字"
						 bordered
						 maxlength="100"
						 disable-default-padding
						 indicator
						 :custom-style="style" />
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			style: 'height: 248rpx',
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
page {
	background: #f5f5f5;
}

.textarea-example {
	padding: 32rpx 32rpx 48rpx;
	background-color: var(--bg-demo-color);
}

.external-class {
	padding-top: 24rpx !important;
	padding-bottom: 24rpx !important;
}

.textarea-example__label {
	display: block;
	color: var(--td-text-color-primary);
	font-size: 24rpx;
	line-height: 40rpx;
	padding-bottom: 16rpx;
}
</style>