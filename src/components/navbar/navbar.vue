<template>
	<view :class="['cy-navbar', setClass, { 'cy-navbar--fixed': fixed }, { 'cy-navbar--dark': dark }, customClass]">
		<view class="cy-navbar__placeholder" :style="setBarStyle" v-if="fixed"></view>
		<view :class="['cy-navbar__content', customClassContent]" :style="setBarStyle">
			<view :class="['cy-navbar__left', customClassLeft]">
				<view class="cy-navbar__btn" v-if="leftArrow" @click="handleBack">
					<cy-icon custom-class="cy-navbar__lefcy-arrow" :name="leftIcon" size="56" />
				</view>
				<slot name="left" />
			</view>
			<view :class="['cy-navbar__center', customClassCenter]" v-if="title || $slots.title">
				<view :class="['cy-navbar__center-title', customClassTitle]">{{ title }}</view>
				<slot name="title" />
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: "navbar",
	externalClasses: ['custom-class', 'custom-class-content', 'custom-class-left', 'custom-class-center', 'custom-class-title'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		title: String,
		fixed: {
			type: Boolean,
			default: true
		},
		leftArrow: Boolean,
		leftIcon: {
			type: String,
			default: 'arrow-left-s-line'
		},
		visible: {
			type: Boolean,
			default: true
		},
		dark: {
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
		customClassLeft: {
			type: [String, Array],
			default: ''
		},
		customClassCenter: {
			type: [String, Array],
			default: ''
		},
		customClassTitle: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			statusBarHeight: 20,
			titleBarHeight: 44,
		}
	},
	computed: {
		setBarStyle() {
			// #ifdef MP-ALIPAY
			return this.fixed ? `padding-top: ${this.statusBarHeight}px; height: ${this.titleBarHeight}px` : `height: ${this.titleBarHeight}px`;
			// #endif
			// #ifdef MP-WEIXIN
			return this.fixed ? `padding-top: ${this.statusBarHeight}px` : '';
			// #endif
		},
		setClass() {
			if (this.visible) {
				return 'cy-navbar--visible cy-navbar--visible-animation'
			} else {
				return 'cy-navbar--hide cy-navbar--hide-animation'
			}
		},
	},
	methods: {
		handleBack(event) {
            const that = this;
			that.$emit('go-back', event);
			uni.navigateBack({
				delta: 1,
				success(e) {
					that.$emit('success', e);
				},
				fail(e) {
					that.$emit('fail', e);
				},
				complete(e) {
					that.$emit('complete', e);
				},
			})
		},
	},
	mounted() {
	},
	watch: {},
	onReady() {
		uni.getSystemInfo({
			success: (info) => {
				this.statusBarHeight = info.statusBarHeight;
				this.titleBarHeight = info.titleBarHeight;
			}
		});
	}
} 
</script>

<style lang="scss">
@import './navbar.scss';
</style>