<template>
	<view v-if="showPopup" class="cy-popup" :class="[popupstyle, isDesktop ? 'fixforpc-z-index' : '', customClass]">
		<view @touchstart="touchstart">
			<cy-transition v-if="maskShow"
						   key="1"
						   name="mask"
						   mode-class="fade"
						   :custom-style="maskStyle"
						   :custom-class="customClassOverlay"
						   :duration="duration"
						   :show="showTrans"
						   @click="onTap" />
			<cy-transition key="2"
						   name="content"
						   :mode-class="ani"
						   :custom-style="transStyle"
						   :custom-class="customClassOverlay"
						   :duration="duration"
						   :show="showTrans"
						   @click="onTap">
				<view class="cy-popup__content" :class="[popupstyle, customClassContent]"
					  @click="clear">
					<view :class="['cy-popup__title', customClassTitle]" v-if="title || $slots.title">
						{{ title }}
						<slot name="title" />
					</view>
					<view v-if="closeBtn" :class="['cy-popup__close', customClassClose]" @click="close">
						<cy-icon name="close-line" size="48" />
						<slot name="close-btn" class="cy-popup__close-slot" />
					</view>
					<slot name="content" />
					<slot />
				</view>
			</cy-transition>
		</view>
	</view>
</template>

<script>
export default {
	name: 'popup',
	emits: ['change', 'maskClick'],
	externalClasses: ['custom-class', 'custom-class-title', 'custom-class-content', 'custom-class-close', 'custom-class-overlay'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		// 是否开启动画
		animation: {
			type: Boolean,
			default: true
		},
		// 弹出方式，可选值，top顶部；bottom底部；left左侧；right右侧；center全屏
		type: {
			type: String,
			default: 'bottom'
		},
		// 蒙版点击是否关闭弹窗
		isMaskClick: {
			type: Boolean,
			default: null
		},
		// TODO 2 个版本后废弃属性 ，使用 isMaskClick
		maskClick: {
			type: Boolean,
			default: null
		},
		// 主窗口背景色
		backgroundColor: {
			type: String,
			default: '#fff'
		},
		// 是否适配底部安全区
		safeArea: {
			type: Boolean,
			default: true
		},
		// 蒙版颜色
		maskBackgroundColor: {
			type: String,
			default: 'rgba(0, 0, 0, 0.55)'
		},
		// 设置圆角(左上、右上、右下和左下)
		radius: {
			type: String,
		},
		// 设置弹窗标题
		title: {
			type: String,
		},
		// 是否显示关闭按钮
		closeBtn: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassTitle: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
		customClassClose: {
			type: [String, Array],
			default: ''
		},
		customClassOverlay: {
			type: [String, Array],
			default: ''
		},
	},

	watch: {
		/**
		 * 监听type类型
		 */
		type: {
			handler: function (type) {
				if (!this.config[type]) return
				this[this.config[type]](true)
			},
			immediate: true
		},
		isDesktop: {
			handler: function (newVal) {
				if (!this.config[newVal]) return
				this[this.config[this.type]](true)
			},
			immediate: true
		},
		/**
		 * 监听遮罩是否可点击
		 * @param {Object} val
		 */
		maskClick: {
			handler: function (val) {
				this.mkclick = val
			},
			immediate: true
		},
		isMaskClick: {
			handler: function (val) {
				this.mkclick = val
			},
			immediate: true
		},
		// H5 下禁止底部滚动
		showPopup(show) {
			// #ifdef H5
			// fix by mehaotian 处理 h5 滚动穿透的问题
			document.getElementsByTagName('body')[0].style.overflow = show ? 'hidden' : 'visible'
			// #endif
		}
	},
	data() {
		return {
			duration: 240,
			ani: [],
			showPopup: false,
			showTrans: false,
			popupWidth: 0,
			popupHeight: 0,
			config: {
				top: 'top',
				bottom: 'bottom',
				center: 'center',
				left: 'left',
				right: 'right',
				message: 'top',
				dialog: 'center',
				share: 'bottom'
			},
			maskStyle: {
				position: 'fixed',
				bottom: 0,
				top: 0,
				left: 0,
				right: 0,
				backgroundColor: 'rgba(0, 0, 0, 0.6)'
			},
			transStyle: {
				backgroundColor: 'transparent',
				radius: this.radius || "0",
				position: 'fixed',
				left: 0,
				right: 0
			},
			maskShow: true,
			mkclick: true,
			popupstyle: 'top'
		}
	},
	computed: {
		getStyles() {
			let res = { backgroundColor: this.bg };
			if (this.radius || "0") {
				res = Object.assign(res, { radius: this.radius })
			}
			return res;
		},
		isDesktop() {
			return this.popupWidth >= 500 && this.popupHeight >= 500
		},
		bg() {
			if (this.backgroundColor === '' || this.backgroundColor === 'none') {
				return 'transparent'
			}
			return this.backgroundColor
		}
	},
	mounted() {
		const fixSize = () => {
			// #ifdef MP-WEIXIN
			const {
				windowWidth,
				windowHeight,
				windowTop,
				safeArea,
				screenHeight,
				safeAreaInsets
			} = uni.getWindowInfo()
			// #endif
			// #ifndef MP-WEIXIN
			const {
				windowWidth,
				windowHeight,
				windowTop,
				safeArea,
				screenHeight,
				safeAreaInsets
			} = uni.getSystemInfoSync()
			// #endif
			this.popupWidth = windowWidth
			this.popupHeight = windowHeight + (windowTop || 0)
			// TODO fix by mehaotian 是否适配底部安全区 ,目前微信ios 、和 app ios 计算有差异，需要框架修复
			if (safeArea && this.safeArea) {
				// #ifdef MP-WEIXIN
				this.safeAreaInsets = screenHeight - safeArea.bottom
				// #endif
				// #ifndef MP-WEIXIN
				this.safeAreaInsets = safeAreaInsets.bottom
				// #endif
			} else {
				this.safeAreaInsets = 0
			}
		}
		fixSize()
		// #ifdef H5
		// window.addEventListener('resize', fixSize)
		// this.$once('hook:beforeDestroy', () => {
		// 	window.removeEventListener('resize', fixSize)
		// })
		// #endif
	},
	// #ifndef VUE3
	// TODO vue2
	destroyed() {
		this.setH5Visible()
	},
	// #endif
	// #ifdef VUE3
	// TODO vue3
	unmounted() {
		this.setH5Visible()
	},
	// #endif
	activated() {
		this.setH5Visible(!this.showPopup);
	},
	deactivated() {
		this.setH5Visible(true);
	},
	created() {
		// this.mkclick =  this.isMaskClick || this.maskClick
		if (this.isMaskClick === null && this.maskClick === null) {
			this.mkclick = true
		} else {
			this.mkclick = this.isMaskClick !== null ? this.isMaskClick : this.maskClick
		}
		if (this.animation) {
			this.duration = 240
		} else {
			this.duration = 0
		}
		// TODO 处理 message 组件生命周期异常的问题
		this.messageChild = null
		// TODO 解决头条冒泡的问题
		this.clearPropagation = false
		this.maskStyle.backgroundColor = this.maskBackgroundColor
	},
	methods: {
		setH5Visible(visible = true) {
			// #ifdef H5
			// fix by mehaotian 处理 h5 滚动穿透的问题
			document.getElementsByTagName('body')[0].style.overflow = visible ? "visible" : "hidden";
			// #endif
		},
		/**
		 * 公用方法，不显示遮罩层
		 */
		closeMask() {
			this.maskShow = false
		},
		/**
		 * 公用方法，遮罩层禁止点击
		 */
		disableMask() {
			this.mkclick = false
		},
		// TODO nvue 取消冒泡
		clear(e) {
			// #ifndef APP-NVUE
			e.stopPropagation()
			// #endif
			this.clearPropagation = true
		},

		open(direction) {
			// fix by mehaotian 处理快速打开关闭的情况
			if (this.showPopup) {
				return
			}
			let innerType = ['top', 'center', 'bottom', 'left', 'right', 'message', 'dialog', 'share']
			if (!(direction && innerType.indexOf(direction) !== -1)) {
				direction = this.type
			}
			if (!this.config[direction]) {
				console.error('缺少类型：', direction)
				return
			}
			this[this.config[direction]]()
			this.$emit('change', {
				show: true,
				type: direction
			})
		},
		close(type) {
			this.showTrans = false
			this.$emit('change', {
				show: false,
				type: this.type
			})
			clearTimeout(this.timer)
			// // 自定义关闭事件
			// this.customOpen && this.customClose()
			this.timer = setTimeout(() => {
				this.showPopup = false
			}, 240)
		},
		// TODO 处理冒泡事件，头条的冒泡事件有问题 ，先这样兼容
		touchstart() {
			this.clearPropagation = false
		},

		onTap() {
			if (this.clearPropagation) {
				// fix by mehaotian 兼容 nvue
				this.clearPropagation = false
				return
			}
			this.$emit('maskClick')
			if (!this.mkclick) return
			this.close()
		},
		/**
		 * 顶部弹出样式处理
		 */
		top(type) {
			this.popupstyle = this.isDesktop ? 'fixforpc-top' : 'top'
			this.ani = ['slide-top']
			this.transStyle = {
				position: 'fixed',
				left: 0,
				right: 0,
				backgroundColor: this.bg,
				radius: this.radius || "0"
			}
			// TODO 兼容 type 属性 ，后续会废弃
			if (type) return
			this.showPopup = true
			this.showTrans = true
			this.$nextTick(() => {
				this.showPoptrans()
				if (this.messageChild && this.type === 'message') {
					this.messageChild.timerClose()
				}
			})
		},
		/**
		 * 底部弹出样式处理
		 */
		bottom(type) {
			this.popupstyle = 'bottom'
			this.ani = ['slide-bottom']
			this.transStyle = {
				position: 'fixed',
				left: 0,
				right: 0,
				bottom: 0,
				paddingBottom: this.safeAreaInsets + 'px',
				backgroundColor: this.bg,
				radius: this.radius || "0",
			}
			// TODO 兼容 type 属性 ，后续会废弃
			if (type) return
			this.showPoptrans()
		},
		/**
		 * 中间弹出样式处理
		 */
		center(type) {
			this.popupstyle = 'center'
			//微信小程序下，组合动画会出现文字向上闪动问题，再此做特殊处理
			// #ifdef MP-WEIXIN
			this.ani = ['fade']
			// #endif
			// #ifndef MP-WEIXIN
			this.ani = ['zoom-out', 'fade']
			// #endif
			this.transStyle = {
				position: 'fixed',
				/* #ifndef APP-NVUE */
				display: 'flex',
				flexDirection: 'column',
				/* #endif */
				bottom: 0,
				left: 0,
				right: 0,
				top: 0,
				justifyContent: 'center',
				alignItems: 'center',
				radius: this.radius || "0"
			}
			// TODO 兼容 type 属性 ，后续会废弃
			if (type) return
			this.showPoptrans()
		},
		left(type) {
			this.popupstyle = 'left'
			this.ani = ['slide-left']
			this.transStyle = {
				position: 'fixed',
				left: 0,
				bottom: 0,
				top: 0,
				backgroundColor: this.bg,
				radius: this.radius || "0",
				/* #ifndef APP-NVUE */
				display: 'flex',
				flexDirection: 'column'
				/* #endif */
			}
			// TODO 兼容 type 属性 ，后续会废弃
			if (type) return
			this.showPoptrans()
		},
		right(type) {
			this.popupstyle = 'right'
			this.ani = ['slide-right']
			this.transStyle = {
				position: 'fixed',
				bottom: 0,
				right: 0,
				top: 0,
				backgroundColor: this.bg,
				radius: this.radius || "0",
				/* #ifndef APP-NVUE */
				display: 'flex',
				flexDirection: 'column'
				/* #endif */
			}
			// TODO 兼容 type 属性 ，后续会废弃
			if (type) return
			this.showPoptrans()
		},
		showPoptrans() {
			this.$nextTick(() => {
				this.showPopup = true
				this.showTrans = true
			})
		}
	}
}
</script>

<style lang="scss">
@import './popup.scss';
</style>