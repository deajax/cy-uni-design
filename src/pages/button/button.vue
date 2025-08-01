<template>
	<div class="button cy-safe-area-bottom">
		<view class="title">基础按钮</view>
		<view class="example">
			<cy-button theme="primary" size="large">填充按钮</cy-button>
			<cy-button theme="light" size="large">填充按钮</cy-button>
			<cy-button size="large">填充按钮</cy-button>
			<cy-button theme="primary" size="large" variant="outline">描边按钮</cy-button>
			<cy-button size="large" variant="text">文字按钮</cy-button>
		</view>

		<view class="title">图标按钮</view>
		<view class="example">
			<cy-button theme="primary" icon="search-line" content="填充按钮" size="large"></cy-button>
			<cy-button theme="primary" size="large" loading>加载中</cy-button>
			<cy-button theme="primary" icon="search-line" shape="square" size="large"></cy-button>
		</view>

		<view class="title">幽灵按钮</view>
		<view class="example" style="padding: 16px; background: #000;">
			<cy-button theme="primary" ghost size="large">幽灵按钮</cy-button>
			<cy-button theme="danger" ghost size="large">幽灵按钮</cy-button>
			<cy-button ghost size="large">幽灵按钮</cy-button>
		</view>

		<view class="title">通栏按钮</view>
		<view class="example">
			<cy-button theme="primary" size="large" block>填充按钮</cy-button>
		</view>

		<view class="title">按钮禁用态</view>
		<view class="example">
			<cy-button theme="primary" size="large" disabled>填充按钮</cy-button>
			<cy-button theme="light" size="large" disabled>填充按钮</cy-button>
			<cy-button size="large" disabled>填充按钮</cy-button>
			<cy-button theme="primary" size="large" variant="outline" disabled>描边按钮</cy-button>
			<cy-button theme="primary" size="large" variant="text" disabled>文字按钮</cy-button>
		</view>

		<view class="title">按钮尺寸</view>
		<view class="example">
			<cy-button theme="primary" icon="search-line" size="large">按钮48</cy-button>
			<cy-button theme="primary" icon="search-line">按钮40</cy-button>
			<cy-button theme="primary" icon="search-line" size="small">按钮32</cy-button>
			<cy-button theme="primary" icon="search-line" size="extra-small">按钮28</cy-button>
		</view>

		<view class="title">按钮形状</view>
		<view class="example">
			<cy-button theme="primary" size="large">填充按钮</cy-button>
			<cy-button theme="primary" size="large" icon="search-line" shape="square"></cy-button>
			<cy-button theme="primary" size="large" shape="round">填充按钮</cy-button>
			<cy-button theme="primary" size="large" icon="search-line" shape="circle"></cy-button>
		</view>
		<view class="example">
			<cy-button theme="primary" size="large" block t-class="external-class">填充按钮</cy-button>
		</view>

		<view class="title">按钮主题</view>
		<view class="example">
			<cy-button size="large">填充按钮</cy-button>
			<cy-button size="large" variant="outline">描边按钮</cy-button>
			<cy-button size="large" variant="text">文字按钮</cy-button>
		</view>

		<view class="example">
			<cy-button size="large" theme="primary">填充按钮</cy-button>
			<cy-button size="large" theme="primary" variant="outline">描边按钮</cy-button>
			<cy-button size="large" theme="primary" variant="text">文字按钮</cy-button>
		</view>

		<view class="example">
			<cy-button size="large" theme="danger">填充按钮</cy-button>
			<cy-button size="large" theme="danger" variant="outline">描边按钮</cy-button>
			<cy-button size="large" theme="danger" variant="text">文字按钮</cy-button>
		</view>

		<view class="example">
			<cy-button size="large" theme="light">填充按钮</cy-button>
			<cy-button size="large" theme="light" variant="outline">描边按钮</cy-button>
			<cy-button size="large" theme="light" variant="text">文字按钮</cy-button>
		</view>

	</div>
</template>

<script>
export default {
	data() {
		return {}
	},
}
</script>

<style lang="scss">
.example {
	padding: 0 16px;
	display: flex;
	flex-wrap: wrap;
	gap: 8px;

	.cy-button {
		margin: 0;
	}
}
</style>