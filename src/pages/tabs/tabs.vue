<template>
	<view class="tabs">
		<view class="mb-4">
			<cy-tabs>
				<cy-tab-panel title="选项1" value="0" />
				<cy-tab-panel title="选项2" value="1" />
			</cy-tabs>
		</view>

		<view class="mb-4">
			<cy-tabs bordered>
				<cy-tab-panel title="选项1" value="0">
					<view class="content">0</view>
				</cy-tab-panel>
				<cy-tab-panel title="选项2" value="1">
					<view class="content">1</view>
				</cy-tab-panel>
				<cy-tab-panel title="上限六个文字" value="2">
					<view class="content">2</view>
				</cy-tab-panel>
			</cy-tabs>
		</view>

		<view class="mb-4">
			<cy-tabs shrink>
				<cy-tab-panel v-for="i in 8" :key="i" :title="'选项' + i" value="i" />
			</cy-tabs>
		</view>

		<view class="mb-4">
			<cy-tabs>
				<cy-tab-panel v-for="i in 4" :key="i" icon="function-line" :title="'选项' + i" value="i" />
			</cy-tabs>
		</view>

		<view class="mb-4">
			<cy-tabs>
				<cy-tab-panel title="选项1" dot value="0" />
				<cy-tab-panel title="选项2" badge="8" value="1" />
				<cy-tab-panel title="上限六个文字" value="2" />
			</cy-tabs>
		</view>

		<view class="mb-4">
			<cy-tabs>
				<cy-tab-panel title="选项1" value="0" />
				<cy-tab-panel title="选项2" value="1" />
				<cy-tab-panel title="选项3" value="2" />
			</cy-tabs>
		</view>

		<view class="mb-4">
			<cy-tabs type="text">
				<cy-tab-panel title="选项1" value="0" />
				<cy-tab-panel title="选项2" value="1" />
				<cy-tab-panel title="选项3" value="2" />
			</cy-tabs>
			<cy-tabs type="card">
				<cy-tab-panel title="选项1" value="0" />
				<cy-tab-panel title="选项2" value="1" />
				<cy-tab-panel title="选项3" value="2" />
			</cy-tabs>
			<cy-tabs type="button">
				<cy-tab-panel title="选项1" value="0" />
				<cy-tab-panel title="选项2" value="1" />
				<cy-tab-panel title="选项3" value="2" />
			</cy-tabs>
			<cy-tabs type="line-button">
				<cy-tab-panel title="选项1" value="0" />
				<cy-tab-panel title="选项2" value="1" />
				<cy-tab-panel title="选项3" value="2" />
			</cy-tabs>
		</view>

		<view class="mb-4">
			<cy-tabs direction="vertical" :animated="false">
				<cy-tab-panel title="选项1" value="0">
					<view class="content">1</view>
				</cy-tab-panel>
				<cy-tab-panel title="选项2" value="1">
					<view class="content">2</view>
				</cy-tab-panel>
				<cy-tab-panel title="选项3" value="2">
					<view class="content">3</view>
				</cy-tab-panel>
			</cy-tabs>
		</view>

		<view class="content">
			<view class="">组件从隐藏状态切换到显示状态时，底部条位置错误？</view>
			<view class="">Tabs 组件在挂载时，会获取自身的宽度，并计算出底部条的位置。如果组件一开始处于隐藏状态，则获取到的宽度永远为 0，因此无法展示底部条位置。</view>
			<view class="">解决方法</view>
			<view class="">方法一，如果是使用 v-show 来控制组件展示的，则替换为 v-if 即可解决此问题：</view>
			<view class="">-- Before --</view>
			<view class="">cy-tabs v-show="show" </view>
			<view class="">-- After --</view>
			<view class="">cy-tabs v-if="show" </view>
			<view class="">方法二，调用组件的 resize 方法来主动触发重绘：</view>
			<view class="">cy-tabs v-show="show" ref="tabs" </view>
			<view class="">this.$refs.tabs.resize();</view>
			<view class="">在popup组件中的tabs组件需resize一次</view>
			<view class="">setTimeout(()=> this.$refs.tabs.resize(),1000)</view>
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
page {
	background: #f5f5f5;
	padding-bottom: 64rpx;
}

.mb-4 {
	margin-bottom: 32rpx;
}

.content {
	padding: 16px;
	background: #fff;
}
</style>