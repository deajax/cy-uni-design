<template>
	<view class="popover">
		<view class="title">基础用法</view>
		<view class="example">
			<cy-popover content="popover">
				<cy-button>点我</cy-button>
			</cy-popover>
		</view>

		<view class="title">自定义颜色</view>
		<view class="example">
			<cy-popover background="red" color="#fff" content="popover">
				<cy-button>点我</cy-button>
			</cy-popover>
		</view>

		<view class="title">自定义位置</view>
		<view class="example">
			<cy-row :gutter="8" :gap="32">
				<cy-col :span="item == 'left' ? 12 : 8" v-for="item in placements" :key="item"
						:custom-class="item == 'left' ? 'align-right' : ''">
					<cy-popover :placement="item">
						<cy-button size="small">{{ item }}</cy-button>
						<template #content>
							<cy-cell left-icon="qr-scan-line" title="扫一扫" />
							<cy-cell left-icon="exchange-cny-fill" title="付钱/收钱" />
							<cy-cell left-icon="qr-code-line" title="乘车码" />
							<cy-cell left-icon="user-add-line" title="添加朋友" :bordered="false" />
						</template>
					</cy-popover>
				</cy-col>
			</cy-row>
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			placements: [
				'top-left',
				'top',
				'top-right',
				'left',
				'right',
				'bottom-left',
				'bottom',
				'bottom-right',
			],
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

.example {
	padding: 0 16px;
}

.align-right {
	text-align: right;
}

.align-center {
	text-align: center;
}
</style>