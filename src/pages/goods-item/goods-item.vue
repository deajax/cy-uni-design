<template>
	<view class="goods-item">
		<view class="title">基础用法</view>
		<view class="example">
			<cy-goods-item image="https://via.placeholder.com/180"
						   title="Apple/苹果 iPhone 15 128GB 黑色"
						   description="企业新客限时专享补贴3000元，更有企业团购低至85折！"
						   price="4899.00"
						   origin-price="5199.00"
						   v-for="i in 2" :key="i">
				<cy-button theme="primary" icon="add-line" size="extra-small" shape="circle" slot="action" />
				<view class="">slot</view>
				<view class="" slot="extra">extra</view>
			</cy-goods-item>
		</view>

		<view class="title">纵向布局</view>
		<view class="example">
			<scroll-view scroll-x>
				<view style="display:flex;gap:12px;flex-wrap:nowrap;width:fit-content;padding:0 16px;">
					<view v-for="i in 6" :key="i" style="width:160px;display:inline-block;">
						<cy-goods-item
									   image="https://via.placeholder.com/180"
									   title="商品标题"
									   description="描述信息"
									   price="2.00"
									   origin-price="3.00"
									   layout="vertical">
							<cy-button icon="add-line" size="extra-small" shape="circle" slot="action" />
						</cy-goods-item>
					</view>
				</view>
			</scroll-view>
		</view>

		<view class="title">圆角</view>
		<view class="example" style="padding: 0 16px;">
			<cy-goods-item image="https://via.placeholder.com/180"
						   title="商品标题"
						   description="描述信息"
						   price="2.00"
						   origin-price="3.00"
						   unit="盒350g"
						   round>
				<cy-button icon="add-line" size="extra-small" shape="circle" slot="action" />
				<view class="baokuan">爆款</view>
				<view class="extra" slot="extra">
					<cy-tag size="small" variant="light" theme="danger">包邮</cy-tag>
					<cy-tag size="small" variant="light" theme="primary">满5000减300</cy-tag>
				</view>
			</cy-goods-item>
		</view>

		<view class="title">带checkbox的列表</view>
		<view class="example">
			<cy-goods-item image="https://via.placeholder.com/180"
						   title="商品标题"
						   description="描述信息"
						   price="2.00"
						   origin-price="3.00"
						   unit="盒350g"
						   v-for="i in 2" :key="i">
				<view class="prefix" slot="prefix">
					<cy-checkbox borderless />
				</view>
			</cy-goods-item>
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
	padding-bottom: var(--safe-area-inset-bottom);
}

.extra {
	margin-top: 6px;
	display: flex;
	gap: 4px;
}

.baokuan {
	position: absolute;
	top: 0;
	left: 0;
	padding: 0 6px 0 4px;
	line-height: 20px;
	background: red;
	color: white;
	font-size: 12px;
	font-weight: 900;
	font-style: italic;
	border-radius: 0 0 8px 0;
}
</style>