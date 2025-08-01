<template>
	<view class="badge">
		<view class="title">红点徽标</view>
		<view class="example">
			<cy-badge dot class="wrapper" content="消息" />
			<cy-badge dot class="wrapper">
				<cy-icon name="notification-4-line" size="48" />
			</cy-badge>
			<cy-badge dot class="wrapper">
				<cy-button>按钮</cy-button>
			</cy-badge>
		</view>

		<view class="title">数字徽标</view>
		<view class="example">
			<cy-badge count="8" content="消息" class="wrapper" />
			<cy-badge count="2" class="wrapper">
				<cy-icon name="notification-4-line" size="48" />
			</cy-badge>
			<cy-badge count="38" class="wrapper">
				<cy-button>按钮</cy-button>
			</cy-badge>
		</view>
		<view class="title">大尺寸</view>
		<view class="example">
			<cy-badge count="8" content="消息" size="large" />
			<cy-badge count="2" size="large">
				<cy-icon name="notification-4-line" size="48" />
			</cy-badge>
			<cy-badge count="38" size="large">
				<cy-button>按钮</cy-button>
			</cy-badge>
		</view>

		<view class="title">自定义徽标</view>
		<view class="example">
			<cy-badge count="NEW">
				<cy-button icon="notification-4-line" shape="square" size="large" />
			</cy-badge>
		</view>

		<view class="title">单独使用</view>
		<cy-cell title="单独使用">
			<cy-badge slot="right-icon" count="23" size="large" />
		</cy-cell>
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
} 
</script>

<style lang="scss">
.example {
	padding: 16px;
	display: flex;
	align-items: center;
	gap: 16px;
}
</style>