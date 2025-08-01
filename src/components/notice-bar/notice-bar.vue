<template>
	<view v-if="visible" :class="['cy-notice-bar', `cy-notice-bar--${theme}`, customClass]" @click.stop="bindClick">
		<view :class="['cy-notice-bar__prefix-icon', customClassPrefixIcon]">
			<slot name="prefix-icon" />
			<cy-icon v-if="prefixIcon" :name="prefixIcon || 'information-fill'"
				custom-class="cy-notice-bar-class-name-icon" />
		</view>

		<view :class="['cy-notice-bar__content-wrap', customClassWrapper]" @longpress="changeAnimationState">
			<view v-if="direction === 'vertical' && Array.isArray(content)">
				<swiper :class="['cy-notice-bar__content--vertical', customClassContent]" :interval="interval" autoplay
					circular vertical>
					<swiper-item v-for="(item, index) in list" :key="index">
						<view :class="['cy-notice-bar__content--vertical-item', customClassItem]">
							{{ item }}
						</view>
					</swiper-item>
				</swiper>
			</view>
			<view v-else
				:class="['cy-notice-bar__content', carousel ? 'cy-notice-bar__marquee' : '', marquee ? '' : 'cy-notice-bar__content-wrapable', animationPlayState ? 'animation-play-running' : 'animation-play-paused', customClassContent]"
				:animation="animationData" :style="[marquee && duration ? { animationDuration: duration } : '']">
				<template v-if="content">{{ content }}</template>
				<slot name="content" />
				<slot />
				<!-- <view :class="['cy-notice-bar__operation', customClassOperation]">
					<template v-if="operation">{{ operation }}</template>
					<slot name="operation" />
				</view> -->
			</view>
		</view>

		<view :class="['cy-notice-bar__suffix-icon', customClassSuffixIcon]" @click.stop="bindSuffix">
			<slot name="suffix-icon" />
			<cy-icon :name="suffixIcon" custom-class="cy-notice-bar-class-suffix-icon" />
		</view>
	</view>
</template>

<script>
export default {
	name: "notice-bar",
	externalClasses: ['custom-class', 'custom-class-prefix-icon', 'custom-class-wrapper', 'custom-class-content', 'custom-class-item', 'custom-class-operation', 'custom-class-suffix-icon'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		content: {
			type: [String, Array],
			default: ''
		},
		direction: {
			type: String,
			default: 'horizontal'
		},
		duration: String,
		operation: String,
		prefixIcon: [String, Boolean],
		suffixIcon: String,
		theme: {
			type: String,
			default: 'info'
		},
		visible: {
			type: Boolean,
			default: true
		},
		interval: {
			type: [String, Number],
			default: 2000
		},
		marquee: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassPrefixIcon: {
			type: [String, Array],
			default: ''
		},
		customClassWrapper: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
		customClassItem: {
			type: [String, Array],
			default: ''
		},
		customClassOperation: {
			type: [String, Array],
			default: ''
		},
		customClassSuffixIcon: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			wrapWidth: 0,
			textWidth: 0,
			list: this.content,
			carousel: false,
			animationPlayState: true,
		}
	},
	computed: {},
	methods: {
		bindClick(e) {
			this.$emit('click', e);
			console.log('noticebar click', e);
		},
		bindSuffix(e) {
			this.$emit('suffix', e);
		},
		changeAnimationState() {
			if (this.animationPlayState) {
				this.animationPlayState = false;
				setTimeout(() => {
					this.animationPlayState = true
				}, 3000)
			}
		},
		getWrapWidth() {
			return new Promise((resolve) => {
				var query = uni.createSelectorQuery().in(this);
				query.select('.cy-notice-bar__content-wrap').boundingClientRect((data) => {
					if (data) {
						this.wrapWidth = data.width;
						console.log('noticeBarWrap', this.wrapWidth);
					}
					resolve();
				}).exec();
			});
		},
		getTextWidth() {
			return new Promise((resolve) => {
				var query = uni.createSelectorQuery().in(this);
				query.select('.cy-notice-bar__content').boundingClientRect((data) => {
					if (data) {
						this.textWidth = data.width;
						console.log('noticeBarText', this.textWidth);
					}
					resolve();
				}).exec();
			});
		}
	},
	watch: {},
	// 组件周期函数--监听组件挂载完毕
	mounted() {
		Promise.all([this.getWrapWidth(), this.getTextWidth()]).then(() => {
			if (this.marquee) {
				if (this.textWidth > this.wrapWidth) {
					this.carousel = true
				} else {
					this.carousel = false
				}
			}
		});
	},

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
@import './notice-bar.scss';
</style>