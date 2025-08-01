<template>
	<view class="checkbox" style="padding-bottom: 80px;">
		<text class="title">基础用法</text>
		<cy-checkbox v-model="checked">复选框</cy-checkbox>

		<text class="title">自定义颜色</text>
		<view style="--cy-brand-color: red">
			<cy-checkbox v-model="colorChecked" primaryColor="#00a231">自定义颜色</cy-checkbox>
		</view>

		<text class="title">自定义图标</text>
		<cy-checkbox icon="lock-line" v-model="iconChecked">自定义图标</cy-checkbox>

		<text class="title">完全自定义图标</text>
		<cy-checkbox v-model="customIconChecked">
			完全自定义图标
			<template slot="icon">
				<image v-if="customIconChecked" style="width: 24px;height: 24px;display: block;" src="/static/logo.png">
				</image>
				<image v-else style="width: 24px;height: 24px;display: block; opacity: .4;" src="/static/logo.png">
				</image>
			</template>
		</cy-checkbox>

		<text class="title">禁用</text>
		<cy-checkbox v-model="disabledChecked" :disabled="true">禁用选中</cy-checkbox>
		<cy-checkbox v-model="disabledUnChecked" :disabled="true">禁用不选中</cy-checkbox>

		<view class="title">横向多选框</view>
		<cy-checkbox-group custom-class="box" borderless @change="onGroupChange" v-model="box">
			<cy-checkbox :name="i" v-for="i in 3" :key="i">标题标题</cy-checkbox>
		</cy-checkbox-group>

		<text class="title">复选框组</text>
		<cy-checkbox-group ref="cGroup" @change="onGroupChange" v-model="color4">
			<view v-for="item in colorList" :key="item.value">
				<cy-checkbox :name="item.value">{{ item.label }}</cy-checkbox>
			</view>
		</cy-checkbox-group>

		<text class="title">全选，反选，清空</text>
		<view class="button-group">
			<button @tap="selectAll">全选</button>
			<button @tap="selectReverse">反选</button>
			<button @tap="clearAll">清空</button>
		</view>
		<cy-checkbox-group ref="cGroup" @change="onGroupChange" v-model="color4">
			<view v-for="item in colorList" :key="item.value">
				<cy-checkbox :name="item.value">{{ item.label }}</cy-checkbox>
			</view>
		</cy-checkbox-group>

		<text class="title">勾选框位置</text>
		<cy-checkbox v-model="checked">复选框</cy-checkbox>
		<cy-checkbox v-model="checked" placement="right">复选框</cy-checkbox>
	</view>
</template>

<script>
export default {
	data() {
		return {
			baseValue: 'base1',
			checked: true,
			colorChecked: true,
			shapeChecked: true,
			sizeChecked: true,
			maxChecked: true,
			iconChecked: true,
			customIconChecked: true,
			disabledChecked: true,
			disabledUnChecked: false,
			box: 0,
			color1: ['green'],
			color2: ['blue'],
			color3: null,
			color4: null,
			color5: null,
			colorPopup1: null,
			colorPopup2: null,
			colorPopup3: null,
			colorPopup4: null,
			colorPopup5: null,
			colorList: [{
				label: '红色',
				value: 'red'
			},
			{
				label: '绿色',
				value: 'green'
			},
			{
				label: '蓝色',
				value: 'blue'
			},
			{
				label: '粉色',
				value: 'pink'
			},
			{
				label: '黑色',
				value: 'black'
			},
			],
		}
	},
	onLoad() {

	},
	methods: {
		onGroupChange(e) {
			console.log(e)
		},
		goNvue() {
			uni.navigateTo({
				url: '/pages/app/app'
			})
		},
		toggleCheckbox1(index) {
			this.$refs.listCheckbox1[index].toggle()
		},
		toggleCheckbox2(index) {
			this.$refs.listCheckbox2[index].toggle()
		},
		selectAll() {
			this.$refs.cGroup.selectAll()
			console.log(this.color4)
		},
		selectReverse() {
			this.$refs.cGroup.selectReverse()
			console.log(this.color4)
		},
		clearAll() {
			this.$refs.cGroup.clearAll()
			console.log(this.color4)
		},
		showIcon(value) {
			return this.color5 && this.color5.includes(value)
		}
	},
}
</script>

<style lang="scss">
.button-group {
	display: flex;
	padding: 0 16px;
	margin-bottom: 16px;
	column-gap: 8px;

	button {
		flex: 1;
		margin: 0;
		padding: 8px;
		line-height: 1;
		height: auto;
		font-size: 14px;
	}
}

.box {
	padding: 32rpx;
	display: flex;
	justify-content: space-between;
	background-color: var(--td-bg-color-container, #fff);
}
</style>