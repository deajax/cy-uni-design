<template>
	<view :class="['cy-row', customClass]" :style="{
		marginLeft: -gutter / 2 + 'px',
		marginRight: -gutter / 2 + 'px',
		rowGap: gap + 'px'
	}">
		<slot />
	</view>
</template>

<script>
export default {
	name: "row",
	externalClasses: ['custom-class'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		gutter: {
			type: [String, Number],
			default: "",
		},
		gap: {
			type: [String, Number],
			default: "",
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {}
	},
	provide() {
		return {
			row: this,
		};
	},
} 
</script>

<style lang="scss">
@import './row.scss';
</style>