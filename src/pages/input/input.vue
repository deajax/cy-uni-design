<template>
	<view class="input">
		<view class="title">基础输入框</view>
		<view class="example">
			<cy-input label="标签文字" placeholder="请输入文字"></cy-input>
			<cy-input label="标签文字" placeholder="请输入文字(选填)" />
			<cy-input placeholder="请输入文字" />
			<cy-input label="标签文字" placeholder="请输入文字" tips="辅助说明" />
		</view>

		<view class="title">带字数限制输入框</view>
		<view class="example">
			<cy-input label="标签文字" placeholder="请输入文字" tips="最大输入10个字符" :maxlength="10" />
			<cy-input label="标签文字" placeholder="请输入文字" tips="最大输入10个字符，汉字算两个" :maxcharacter="10" />
		</view>

		<view class="title">带操作输入框</view>
		<view class="example">
			<cy-input
					  label="标签文字"
					  placeholder="请输入文字"
					  :suffixIcon="{ name: 'error-warning-fill', ariaLabel: '提示' }" />
			<cy-input label="标签文字" placeholder="请输入手机号码">
				<cy-button slot="suffix" theme="primary" size="extra-small"> 操作按钮 </cy-button>
			</cy-input>
			<cy-input label="标签文字" placeholder="请输入文字" :suffixIcon="{ name: 'user-line', ariaLabel: '通讯录' }" />
		</view>

		<view class="title">带图标输入框</view>
		<view class="example">
			<cy-input prefixIcon="apps-line" label="标签文字" placeholder="请输入文字" />
			<cy-input prefixIcon="apps-line" placeholder="请输入文字" />
		</view>

		<view class="title">特定类型输入框</view>
		<view class="example">
			<cy-input label="输入密码" type="password" :value="textPassword" clearable />
			<cy-input placeholder="输入验证码" label="验证码">
				<view slot="suffix" class="suffix">
					<cy-divider layout="vertical" />
					<image
						   class="image"
						   src="https://wwcdn.weixin.qq.com/node/wework/images/202010241547.ac6876be9c.png"
						   mode="heightFix"
						   aria-role="img"
						   aria-label="验证码" />
				</view>
			</cy-input>

			<cy-input
					  label="手机号"
					  placeholder="输入手机号码"
					  :value="phoneNumber"
					  type="number"
					  :tips="phoneError ? '手机号输入不正确' : ''">
				<view slot="suffix" style="display: flex; align-items: center">
					<cy-divider layout="vertical" />
					<view class="verify" aria-role="button"> 发送验证码 </view>
				</view>
			</cy-input>

			<cy-input
					  label="价格"
					  placeholder="0.00"
					  suffix="元"
					  align="right"
					  type="number"
					  :tips="priceError ? '请输入正确的价格' : ''"
					  custom-class-tips="tips" />

			<cy-input label="数量" placeholder="填写个数" suffix="个" align="right" type="number" />

		</view>

		<view class="title">输入框状态</view>
		<view class="example">
			<cy-input label="标签文字" placeholder="请输入文字" value="已输入文字" status="error" tips="辅助说明" />
			<cy-input label="标签文字" value="不可编辑文字" disabled />
		</view>

		<view class="title">信息超长状态</view>
		<view class="example">
			<cy-input label="标签超长时最多十个字" placeholder="请输入文字" />
		</view>

		<view class="title">内容位置</view>
		<view class="example">
			<cy-input label="左对齐" placeholder="请输入文字" />
			<cy-input label="居中" placeholder="请输入文字" align="center" />
			<cy-input label="右对齐" placeholder="请输入文字" align="right" />
		</view>

		<view class="title">竖排样式</view>
		<view class="example">
			<cy-input
					  label="标签文字"
					  layout="vertical"
					  placeholder="请输入文字"
					  :suffixIcon="{ name: 'error-warning-fill', ariaLabel: '提示' }"></cy-input>

		</view>

		<view class="title">标签外置样式</view>
		<view class="example">
			<view class="input-example">
				<view class="input-example__label">标签文字</view>
				<cy-input
						  placeholder="请输入文字"
						  borderless
						  :suffixIcon="{ name: 'error-circle-filled', ariaLabel: '提示' }"
						  :style="style" />
			</view>
		</view>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			value: '',
			textPassword: '123456',
			phoneError: false,
			phoneNumber: '17600600600',
			priceError: false,
			style: 'border: 2rpx solid #f3f3f3; border-radius: 12rpx;',
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
	padding-bottom: var(--safe-area-inset-bottom);
}

.suffix {
	display: flex;
	align-items: center;
}

.image {
	width: 72px;
	height: 36px;
	display: block;
	margin-top: -6px;
	margin-bottom: -6px;
}

.tips {
	text-align: right !important;
}

.verify {
	color: var(--cy-brand-color, #0052D9);
	font-size: 32rpx;
}

.input-example {
	--cy-input-vertical-padding: 24rpx;

	background-color: #fff;
	padding: 32rpx;
}

.input-example__label {
	color: var(--cy-text-color-primary);
	font-size: 28rpx;
	line-height: 40rpx;
	margin: 0 8rpx 16rpx;
}
</style>