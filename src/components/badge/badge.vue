<template>
	<view :class="['cy-badge', `cy-badge--${size}`, customClass]">
		<!-- #ifdef MP-ALIPAY -->
		<view :class="['cy-badge__content', customClassContent]" v-if="$slots.$default || content">
			<view class="cy-badge__content-text">{{ content }}</view>
			<slot class="cy-badge__content-slot" />
		</view>
		<view :class="['cy-badge__count', $slots.$default || content ? '' : 'cy-badge--empty', customClassCount]"
			  v-if="dot || count">
			<view class="cy-badge__count-dot" v-if="dot"></view>
			<view class="cy-badge__count-text" :style="setStyle" v-else>{{ count }}</view>
			<slot name="count" v-if="!dot" />
		</view>
		<!-- #endif -->

		<!-- #ifndef MP-ALIPAY -->
		<view :class="['cy-badge__content', customClassContent]" v-if="$slots.default || content">
			<view class="cy-badge__content-text">{{ content }}</view>
			<slot class="cy-badge__content-slot" />
		</view>
		<view :class="['cy-badge__count', $slots.default || content ? '' : 'cy-badge--empty', customClassCount]"
			  v-if="dot || count">
			<view class="cy-badge__count-dot" v-if="dot"></view>
			<view class="cy-badge__count-text" :style="[setStyle]" v-else>{{ count }}</view>
			<slot name="count" v-if="!dot" />
		</view>
		<!-- #endif -->
		<slot name="badge" />
	</view>
</template>

<script>
export default {
	name: "badge",
	externalClasses: ['custom-class', 'custom-class-count', 'custom-class-content'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		color: {
			type: String,
			default: ''
		},
		content: {
			type: String,
			default: ''
		},
		count: {
			type: [String, Number],
			default: ''
		},
		dot: {
			type: Boolean,
			default: false
		},
		size: {
			type: String,
			default: 'medium'
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
		customClassCount: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {
		setStyle() {
			return { backgroundColor: this.color }
		}
	},
	methods: {},
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
@import './badge.scss';
</style>