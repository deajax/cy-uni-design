<template>
	<view class="cy-sticky" :style="style">
		<slot></slot>
	</view>
</template>

<script>
export default {
	name: "sticky",
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		zIndex: {
			type: [String, Number],
			default: 99,
		},
		offsetTop: {
			type: [String, Number],
			default: '',
		},
	},
	computed: {
		style() {
			let style = 'z-index: ' + this.zIndex + ';';
			if (this.offsetTop) {
				style += `top: ${this.offsetTop}px`;
			}
			return style;
		}
	},
	data() {
		return {};
	}
}
</script>

<style lang="scss">
@import './sticky.scss';
</style>