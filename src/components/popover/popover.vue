<template>
	<view :class="['cy-popover', `cy-popover--${placement}`, customClass]">
		<view @click.stop="onVisibleChange">
			<slot></slot>
		</view>
		<template v-if="show">
			<view :class="['cy-popover__content', $slots.content ? 'cy-popover__content-custom' : '', customClassContent]"
				  :style="setContentStyle">
				<template v-if="content">
					{{ content }}
				</template>
				<slot name="content"></slot>
			</view>
			<view class="cy-popover__arrow" :style="{ borderColor: background }"></view>
		</template>
		<view v-if="show" :class="['cy-popover__overlay', customClassOverlay]" @click="handleOverlay" />
	</view>
</template>

<script>
export default {
	name: "popover",
	externalClasses: ['custom-class', 'custom-class-content'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		background: String,
		color: String,
		content: String,
		placement: {
			type: String,
			default: 'top'
		},
		visible: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			show: this.visible
		}
	},
	computed: {
		setContentStyle() {
			return `background: ${this.background}; color: ${this.color}`
		}
	},
	methods: {
		onVisibleChange() {
			this.show = !this.show
		},
		handleOverlay() {
			this.show = false;
			this.stop && this.preventEvent(e);
		},
	},
	watch: {},

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
@import './popover.scss';
</style>