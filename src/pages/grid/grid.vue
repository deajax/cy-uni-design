<template>
	<view class="grid">
		<view class="title">基础宫格</view>
		<view class="example">
			<cy-grid class="block" :column="5">
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="最多四字" :image="img" />
			</cy-grid>

			<cy-grid class="block">
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="最多五个字" :image="img" />
			</cy-grid>

			<cy-grid class="block" :column="3">
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="最多六个文字" :image="img" />
			</cy-grid>
		</view>

		<view class="title">带说明的宫格</view>
		<view class="example">
			<view class="block">
				<cy-grid column="3">
					<cy-grid-item text="标题文字" description="描述文字" :image="img" />
					<cy-grid-item text="标题文字" description="描述文字" :image="img" />
					<cy-grid-item text="标题文字" description="描述文字" :image="img" />
				</cy-grid>
			</view>

			<view class="block">
				<cy-grid column="2" align="left">
					<cy-grid-item text="标题文字" description="描述文字" layout="horizontal" :image="img" />
					<cy-grid-item text="标题文字" description="描述文字" layout="horizontal" :image="img" />
				</cy-grid>
			</view>
		</view>

		<view class="title">带边框的宫格</view>
		<view class="example">
			<view class="block">
				<cy-grid bordered column="3">
					<cy-grid-item text="标题文字" :image="img" />
					<cy-grid-item text="标题文字" :image="img" />
					<cy-grid-item text="标题文字" :image="img" />
				</cy-grid>
			</view>

			<view class="block">
				<cy-grid bordered column="2" align="left">
					<cy-grid-item text="标题文字" description="描述文字" layout="horizontal" :image="img" />
					<cy-grid-item text="标题最多六字" description="描述文字" layout="horizontal" :image="img" />
				</cy-grid>
			</view>
		</view>

		<view class="title">带徽章的宫格</view>
		<view class="example">
			<cy-grid class="cy-grid badge">
				<cy-grid-item text="标题文字" :image="img" :badge-props="{ dot: true }" />
				<cy-grid-item text="标题文字" :image="img" :badge-props="{ count: 8 }" />
				<cy-grid-item text="标题文字" :image="img" :badge-props="{ count: 13 }" />
				<cy-grid-item text="标题文字" :image="img" :badge-props="{ count: 'NEW' }" />
			</cy-grid>
		</view>

		<view class="title">可滑动的宫格</view>
		<view class="example">
			<cy-grid class="block" column="0">
				<cy-grid-item v-for="i in 8" :key="i" text="最多五个字" :image="img" />
			</cy-grid>
		</view>

		<view class="title">可传图标的宫格</view>
		<view class="example">
			<cy-grid class="block">
				<cy-grid-item text="分享" icon="share-line" bindclick="onClick" />
				<cy-grid-item text="收藏" icon="star-line" bindclick="onClick" />
				<cy-grid-item text="保存" icon="import-line" bindclick="onClick" />
				<cy-grid-item text="编辑" icon="draft-line" bindclick="onClick" />
			</cy-grid>
		</view>

		<view class="title">多行宫格</view>
		<view class="example">
			<cy-grid class="block" column="4">
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="最多五个字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="最多五个字" :image="img" />
			</cy-grid>
		</view>

		<view class="title">卡片宫格</view>
		<view class="example">
			<cy-grid class="block" column="4" theme="card">
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="最多五个字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="标题文字" :image="img" />
				<cy-grid-item text="最多五个字" :image="img" />
			</cy-grid>
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			img: 'https://via.placeholder.com/80',
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
	padding-bottom: 80px;
}

.block {
	margin-bottom: 16px;
}
</style>