<template>
	<view class="radio" style="padding-bottom: 80px;">
		<view class="title">基础用法</view>
		<cy-radio v-model="baseValue" name="base1">基础用法1</cy-radio>
		<cy-radio v-model="baseValue" name="base2">基础用法2</cy-radio>

		<view class="title">自定义颜色</view>
		<view style="--cy-brand-color: red">
			<cy-radio v-model="primaryColorValue" name="primaryColor1">自定义颜色1</cy-radio>
			<cy-radio v-model="primaryColorValue" name="primaryColor2">自定义颜色2</cy-radio>
		</view>

		<view class="title">自定义图标</view>
		<cy-radio v-model="uniValue" icon="lock-line" name="uni1">自定义图标1</cy-radio>
		<cy-radio v-model="uniValue" icon="lock-line" name="uni2">自定义图标2</cy-radio>

		<view class="title">完全自定义图标</view>
		<cy-radio v-model="iconValue" name="icon1">
			<text>完全自定义图标1</text>
			<template slot="icon">
				<text :style="{ color: iconValue === 'icon1' ? '#f00' : '#ccc' }">1</text>
			</template>
		</cy-radio>
		<cy-radio v-model="iconValue" name="icon2">
			<text>完全自定义图标2</text>
			<template slot="icon">
				<text :style="{ color: iconValue === 'icon2' ? '#f00' : '#ccc' }">2</text>
			</template>
		</cy-radio>

		<view class="title">自定义大小</view>
		<cy-radio v-model="sizeValue" :iconSize="30" :titleStyle="{ 'font-size': '22px', color: 'red' }"
				  name="size1">自定义大小1</cy-radio>
		<cy-radio v-model="sizeValue" :iconSize="30" :titleStyle="{ 'font-size': '22px', color: 'red' }"
				  name="size2">自定义大小2</cy-radio>

		<view class="title">禁用</view>
		<cy-radio v-model="disabledValue" :disabled="true" name="disabled1">禁用1</cy-radio>
		<cy-radio v-model="disabledValue" :disabled="true" name="disabled2">禁用2</cy-radio>

		<view class="title">横向单选框</view>
		<cy-radio-group custom-class="box" borderless @change="onGroupChange" v-model="color1">
			<view v-for="item in 3" :key="item">
				<cy-radio :name="item">标题标题</cy-radio>
			</view>
		</cy-radio-group>

		<view class="title">单选框组</view>
		<cy-radio-group @change="onGroupChange" v-model="color1">
			<view v-for="item in colorList" :key="item.value">
				<cy-radio :name="item.name">{{ item.label }}</cy-radio>
			</view>
		</cy-radio-group>

		<view class="title">选中项可以取消</view>
		<cy-radio-group @change="onGroupChange" v-model="colorClear">
			<view v-for="item in colorList" :key="item.value">
				<cy-radio clearable :name="item.name">{{ item.label }}</cy-radio>
			</view>
		</cy-radio-group>

		<view class="title">勾选框位置</view>
		<cy-radio v-model="baseValue" name="base1">基础用法1</cy-radio>
		<cy-radio v-model="baseValue" name="base2" placement="right">基础用法2</cy-radio>
	</view>
</template>

<script>
export default {
	data() {
		return {
			radioValue: 'base',
			baseValue: 'base1',
			primaryColorValue: 'primaryColor1',
			shapeValue: 'shape1',
			uniValue: 'uni1',
			iconValue: 'icon1',
			sizeValue: 'size1',
			disabledValue: 'disabled1',
			color1: 'red',
			color2: 'green',
			color3: 'blue',
			colorClear: 'red',
			colorList: [{
				label: '红色',
				name: 'red'
			},
			{
				label: '绿色',
				name: 'green'
			},
			{
				label: '蓝色',
				name: 'blue'
			},
			{
				label: '粉色',
				name: 'pink'
			},
			{
				label: '黑色',
				name: 'black'
			},
			]
		}
	},
	onLoad() {

	},
	methods: {
		onGroupChange(e) {
			console.log(e)
		},
	}
}
</script>

<style lang="scss">
.cy-radio-show {
	padding: 20px;

	&__title {
		padding: 10px 0;

		&__item {
			font-size: 16px;
			color: #333;
			font-weight: bold;
		}
	}

	&__group-item {
		margin-bottom: 10px;
	}

	&__list-item {
		display: flex;
		align-items: center;
		height: 50px;
		border-bottom: 1px solid #eee;

		&__name {
			font-size: 16px;
			color: #333;
			flex: 1;
			margin-right: 6px;
		}
	}

	.custom-radio {
		::v-deep {
			.cy-radio {
				height: 50px;
				border-bottom: 1px solid #eee;
				flex-direction: row-reverse;

				&__name {
					flex: 1;
				}
			}
		}
	}
}

.box {
	padding: 32rpx;
	display: flex;
	justify-content: space-between;
	background-color: var(--td-bg-color-container, #fff);
}
</style>
