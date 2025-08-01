<template>
	<view class="text">
		<view class="title">基础文字链接</view>
		<view class="example">
			<cy-text size="small" theme="primary" content="文本内容" hover />
			<cy-text size="small" content="文本内容" />
		</view>

		<view class="title">下划线文字链接</view>
		<view class="example">
			<cy-text size="small" theme="primary" content="文本内容" underline hover />
			<cy-text size="small" content="文本内容" underline />
		</view>

		<view class="title">前置图标文字链接</view>
		<view class="example">
			<cy-text size="small" theme="primary" content="文本内容" prefixIcon="links-line" hover />
			<cy-text size="small" content="文本内容" prefixIcon="links-line" />
		</view>

		<view class="title">后置图标文字链接</view>
		<view class="example">
			<cy-text size="small" theme="primary" content="文本内容" suffixIcon="share-line" hover />
			<cy-text size="small" content="文本内容" suffixIcon="share-line" />
		</view>

		<view class="title">不同主题</view>
		<view class="example">
			<cy-text size="small" theme="primary" content="文本内容" suffixIcon="share-line" />
			<cy-text size="small" content="文本内容" suffixIcon="share-line" />
			<cy-text size="small" theme="danger" content="文本内容" suffixIcon="share-line" />
			<cy-text size="small" theme="warning" content="文本内容" suffixIcon="share-line" />
			<cy-text size="small" theme="success" content="文本内容" suffixIcon="share-line" />
		</view>

		<view class="title">禁用状态</view>
		<view class="example">
			<cy-text
					 size="small"
					 theme="primary"
					 content="文本内容"
					 suffixIcon="share-line"
					 disabled />
			<cy-text size="small" content="文本内容" suffixIcon="share-line" disabled />
			<cy-text size="small" theme="danger" content="文本内容" suffixIcon="share-line" disabled />
			<cy-text size="small" theme="warning" content="文本内容" suffixIcon="share-line" disabled />
			<cy-text size="small" theme="success" content="文本内容" suffixIcon="share-line" disabled />
		</view>

		<view class="title">组件尺寸</view>
		<view class="example">
			<cy-text size="small" theme="primary" content="S号链接" suffixIcon="share-line" />
			<cy-text theme="primary" content="M号链接" suffixIcon="share-line" />
			<cy-text size="large" theme="primary" content="L号链接" suffixIcon="share-line" />
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
.example {
	padding: 0 16px;

	.cy-text {
		margin-right: 16px;
	}
}
</style>