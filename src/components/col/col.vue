<template>
	<view :class="['cy-col', setSpan, setOffset, customClass]" :style="setGutter">
		<slot></slot>
	</view>
</template>

<script>
export default {
	name: "col",
	externalClasses: ['custom-class'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	inject: ["row"],
	props: {
		span: {
			type: [Number, String],
			default: "",
		},
		offset: {
			type: [Number, String],
			default: 0,
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			gutter: 0,
		};
	},
	created() {
		this.gutter = this.row.gutter / 2;
	},
	computed: {
		setSpan() {
			if (!this.span || this.span < 1) return "";
			else if (this.span > 24) return "cy-col--24";
			else return "cy-col--" + this.span;
		},
		setOffset() {
			if (this.offset >= 1 && this.offset < 24)
				return "cy-col--offset-" + this.offset;
			else return "";
		},
		setGutter() {
			if (this.gutter != "0" ||  this.gutter > "0") return "padding: 0 " + this.gutter + "px";
			else return "";
		},
	},
	methods: {},

	// 组件周期函数--监听组件挂载完毕
	mounted() { },
	// 组件周期函数--监听组件数据更新之前
	beforeUpdate() { },
	// 组件周期函数--监听组件数据更新之后
	updated() { },
	// 组件周期函数--监听组件激活(显示)
	activated() { },
	// 组件周期函数--监听组件停用(隐藏)
	deactivated() { },
	// 组件周期函数--监听组件销毁之前
	beforeDestroy() { },
} 
</script>

<style lang="scss">
@import './col.scss';
</style>