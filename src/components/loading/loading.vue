<template>
	<view :class="['cy-loading', `cy-loading--${layout}`, customClass]">
		<view :class="['cy-loading__spinner', `cy-loading__spinner--${theme}`, customClassIndicator]"
			  :style="[indicatorStyle]"
			  v-if="indicator || $slots.indicator">
			<view class="cy-loading__circular" v-if="theme === 'circular'"></view>
			<slot name="indicator" />
		</view>
		<view :class="['cy-loading__text', `cy-loading__text--${layout}`, customClassText]" v-if="text || $slots.text">
			{{ text }}
			<slot name="text" />
		</view>
		<slot />
	</view>
</template>

<script>
export default {
	name: "loading",
	externalClasses: ['custom-class', 'custom-class-indicator', 'custom-class-circular', 'custom-class-text'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		text: String,
		color: String,
		layout: {
			type: String,
			default: 'horizontal'
		},
		theme: {
			type: String,
			default: 'circular'
		},
		indicator: {
			type: Boolean,
			default: true
		},
		duration: {
			type: [String, Number],
			default: '800'
		},
		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassIndicator: {
			type: [String, Array],
			default: ''
		},
		customClassCircular: {
			type: [String, Array],
			default: ''
		},
		customClassText: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {
		indicatorStyle() {
			return {
				color: `${this.color}`,
				animationDuration: `${this.duration / 1000}s`,
			};
		}
	},
} 
</script>

<style lang="scss">
@import './loading.scss';
</style>