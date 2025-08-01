<template>
	<view class="avatar">
		<view class="title">图片头像</view>
		<view class="example">
			<cy-avatar :image="image" />
			<cy-avatar shape="round" :image="image" />
		</view>

		<view class="title">字符头像</view>
		<view class="example">
			<cy-avatar>A</cy-avatar>
			<cy-avatar shape="round">A</cy-avatar>
		</view>

		<view class="title">图标头像</view>
		<view class="example">
			<cy-avatar icon="user-line" />
			<cy-avatar shape="round" icon="user-line" />
		</view>

		<view class="title">组合头像</view>
		<view class="example">
			<view class="avatar-example">
				<cy-avatar-group max="5" collapseAvatar="+5">
					<cy-avatar v-for="i in 5" :key="i" :image="image" bordered />
				</cy-avatar-group>
			</view>
			<view class="avatar-example">
				<cy-avatar-group max="5" cascading="right-up">
					<cy-avatar v-for="i in 5" :key="i" :image="image" bordered />
				</cy-avatar-group>
			</view>
		</view>

		<view class="title">徽标头像</view>
		<view class="example">
			<cy-avatar :image="image" :badge-props="{ dot: true }" />
			<cy-avatar :badge-props="{ count: 8 }">A</cy-avatar>
			<cy-avatar icon="user-line" :badge-props="{ count: 12 }" />
		</view>

		<view class="title">头像尺寸</view>
		<view class="example">
			<view class="avatar-example">
				<cy-avatar :image="image" size="large" />
				<cy-avatar size="large">A</cy-avatar>
				<cy-avatar icon="user-line" size="large" />
			</view>

			<view class="avatar-example">
				<cy-avatar :image="image" />
				<cy-avatar size="medium">A</cy-avatar>
				<cy-avatar icon="user-line" size="medium" />
			</view>

			<view class="avatar-example">
				<cy-avatar :image="image" size="small" />
				<cy-avatar size="small">A</cy-avatar>
				<cy-avatar icon="user-line" size="small" />
			</view>
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			image: 'https://via.placeholder.com/80'
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
}
</style>