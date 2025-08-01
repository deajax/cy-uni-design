<template>
	<view :class="layout === 'vertical' ? 'cy-divider--vertical-center' : ''">
		<view :class="['cy-divider', customClass, setClass, `cy-divider--${layout}`, `cy-divider--${align}`]">
			<view :class="['cy-divider__content', customClassContent]">
				<view v-if="content">{{ content }}</view>
				<slot v-else name="content" />
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: "divider",
	externalClasses: ['custom-class', 'custom-class-content'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		align: {
			type: String,
			default: 'center'
		},
		content: String,
		dashed: Boolean,
		layout: {
			type: String,
			default: 'horizontal'
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
		return {}
	},
	computed: {
		setClass() {
			if (this.dashed) {
				return 'cy-divider--dashed'
			}
		},
	},
} 
</script>

<style lang="scss">
@import './devider.scss';
</style>