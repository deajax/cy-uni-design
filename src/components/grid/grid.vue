<template>
	<view :class="['cy-grid', { 'cy-grid--card': theme === 'card' }, customClass]">
		<view v-if="column > 0" :class="['cy-grid__content', customClassContent]" :style="contentStyle">
			<slot></slot>
		</view>
		<view v-else :class="['cy-grid__content', customClassContent]">
			<scroll-view scroll-x scroll-with-animation :scroll-left="scrollLeft"
				:class="['cy-grid__scroll-view', customClassScrollView]" :style="'white-space: nowrap;' + contentStyle"
				@scroll="handleScroll">
				<view class="cy-grid__scroll-wrapper">
					<slot></slot>
				</view>
			</scroll-view>
			<view class="cy-grid__indicator" v-if="indicator">
				<view class="cy-grid__indicator--line">
					<view class="cy-grid__indicator--line-bar" :style="{ transform: `translateX(${scrollValue}%)` }">
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: "grid",
	externalClasses: ['custom-class', 'custom-class-content', 'custom-class-scroll-view'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		/** 内容对齐方式 */
		align: {
			type: String,
			default: 'center',
		},
		/** 边框，默认不显示。值为 true 则显示默认边框，值类型为 object 则表示自定义边框样式 */
		bordered: {
			type: null,
			default: false,
		},
		/** 每一行的列数量；为 0 时等于固定大小 */
		column: {
			type: [Number, String],
			default: 4,
		},
		/** 间隔大小 */
		gutter: {
			type: Number,
		},
		/** 是否开启点击反馈 */
		hover: {
			type: Boolean,
			default: false,
		},
		/** 宫格的风格 */
		theme: {
			type: String,
			default: 'default',
		},
		scrollLeft: {
			type: [Number, String],
		},
		/** 滑动宫格的滚动条 */
		indicator: {
			type: Boolean,
			default: true,
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
		customClassScrollView: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			scrollValue: 0,
			elementWidth: 375
		}
	},
	provide() {
		return {
			grid: this
		};
	},
	computed: {
		contentStyle() {
			return this.bordered ? 'margin-left: -1px; margin-top: -1px;' : '',
				this.gutter ? `margin-left: -${this.gutter * 2}rpx; margin-top: -${this.gutter * 2}rpx;` : '';
		}
	},
	methods: {
		getElementInfo() {
			const query = uni.createSelectorQuery().in(this);
			query.select('.cy-grid').boundingClientRect(data => {
				if (data) {
					this.elementWidth = data.width
				}
			}).exec();
		},
		handleScroll(e) {
			this.scrollValue = e.detail.scrollLeft / (e.detail.scrollWidth - this.elementWidth) * 100
		}
	},
	watch: {},

	// 组件周期函数--监听组件挂载完毕
	mounted() {
		this.getElementInfo();
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
@import './grid.scss';
</style>