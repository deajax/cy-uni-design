<template>
	<view class="notice-bar">
		<view class="title">纯文字的公告栏</view>
		<view class="example">
			<cy-notice-bar content="这是一条普通的通知信息" :prefixIcon="false"></cy-notice-bar>
		</view>

		<view class="title">带图标的公告栏</view>
		<view class="example">
			<cy-notice-bar :prefixIcon="false" content="提示文字描述提示文字描述提示文字描述">
				<view slot="prefix-icon">
					<cy-icon name="information-fill"></cy-icon>
				</view>
			</cy-notice-bar>
		</view>

		<view class="title">带关闭的公告栏</view>
		<view class="example">
			<cy-notice-bar suffix-icon="close-line" content="这是一条普通的通知信息" />
		</view>

		<view class="title">带入口的公告栏</view>
		<view class="example">
			<cy-notice-bar suffix-icon="arrow-right-s-line">
				<view slot="content" style="display: inline-flex;">
					<text>这是一条普通的通知信息</text>
					<cy-text content="详情" theme="primary" />
				</view>
			</cy-notice-bar>
		</view>

		<view class="title">组件状态</view>
		<view class="example">
			<cy-notice-bar prefix-icon="information-fill" content="默认状态公告栏默认状态公告栏"></cy-notice-bar>
			<cy-notice-bar prefix-icon="checkbox-circle-fill" theme="success" content="成功状态公告栏成功状态公告栏"></cy-notice-bar>
			<cy-notice-bar prefix-icon="information-fill" theme="warning" content="警示状态公告栏警示状态公告栏"></cy-notice-bar>
			<cy-notice-bar prefix-icon="information-fill" theme="error" content="错误状态公告栏错误状态公告栏"></cy-notice-bar>
		</view>

		<view class="title">可滚动公告栏</view>
		<view class="example">
			<cy-notice-bar prefix-icon="volume-up-line" content="君不见高堂明镜悲白发，朝如青丝暮成雪，人生得意须尽欢" theme="error" marquee />
			<cy-notice-bar prefix-icon="volume-up-line" :content="content" direction="vertical" />
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			content: ['君不见高堂明镜悲白发', '朝如青丝暮成雪', '人生得意须尽欢', '莫使金樽空对月']
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
	padding-bottom: 64rpx;
}
</style>