<template>
	<view :class="['cy-card', `cy-card--${theme}`, customClass]">
		<view :class="['cy-card__header']" v-if="title || $slots.title || extra || $slots.extra">
			<view :class="['cy-card__title', customClassTitle]" v-if="title || $slots.title">
				<slot name="title" />
				{{ title }}
			</view>
			<view :class="['cy-card__extra', customClassExtra]" v-if="extra || $slots.extra">
				<slot name="extra" />
				{{ extra }}
			</view>
		</view>
		<view :class="['cy-card__content', customClassContent]" v-if="$slots.default">
			<slot />
		</view>
		<view :class="['cy-card__action', customClassAction]" v-if="$slots.action">
			<slot name="action" />
		</view>
	</view>
</template>

<script>
export default {
	name: "card",
	externalClasses: ['custom-class', 'custom-class-title', 'custom-class-extra', 'custom-class-action', 'custom-class-content'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		theme: {
			type: String,
			default: 'default'
		},
		title: String,
		extra: String,
		
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassTitle: {
			type: [String, Array],
			default: ''
		},
		customClassExtra: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
		customClassAction: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {},
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
@import './card.scss';
</style>