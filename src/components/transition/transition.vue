<template>
	<view
		  v-show="isShow"
		  ref="ani"
		  :animation="animationData"
		  :class="['cy-transition', customClass]"
		  :style="transformStyles"
		  @click="onClick">
		<slot></slot>
	</view>
</template>

<script>
import { createAnimation } from './createAnimation'

export default {
	name: 'transition',
	emits: ['click', 'change'],
	externalClasses: ['customClass'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		// 控制组件显示或隐藏
		show: {
			type: Boolean,
			default: false
		},
		// [fade|slide-top|slide-right|slide-bottom|slide-left|zoom-in|zoom-out] 过渡动画类型
		modeClass: {
			type: [Array, String],
			default() {
				return 'fade'
			}
		},
		// 过渡动画持续时间
		duration: {
			type: Number,
			default: 240
		},
		customStyle: {
			type: Object,
			default() {
				return {}
			}
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			isShow: false,
			transform: '',
			opacity: 1,
			animationData: {},
			durationTime: 240,
			config: {}
		}
	},
	watch: {
		show: {
			handler(newVal) {
				if (newVal) {
					this.open()
				} else {
					// 避免上来就执行 close,导致动画错乱
					if (this.isShow) {
						this.close()
					}
				}
			},
			immediate: true
		}
	},
	computed: {
		// 生成样式数据
		stylesObject() {
			let customStyle = {
				...this.customStyle,
				'transition-duration': this.duration / 1000 + 's'
			}
			let transform = ''
			for (let i in customStyle) {
				let line = this.toLine(i)
				transform += line + ':' + customStyle[i] + ';'
			}
			return transform
		},
		// 初始化动画条件
		transformStyles() {
			return 'transform:' + this.transform + ';' + 'opacity:' + this.opacity + ';' + this.stylesObject
		}
	},
	created() {
		// 动画默认配置
		this.config = {
			duration: this.duration,
			timingFunction: 'ease',
			transformOrigin: '50% 50%',
			delay: 0
		}
		this.durationTime = this.duration
	},
	methods: {
		/**
		 *  ref 触发 初始化动画
		 */
		init(obj = {}) {
			if (obj.duration) {
				this.durationTime = obj.duration
			}
			this.animation = createAnimation(Object.assign(this.config, obj), this)
		},
		/**
		 * 点击组件触发回调
		 */
		onClick() {
			this.$emit('click', {
				detail: this.isShow
			})
		},
		/**
		 * ref 触发 动画分组
		 * @param {Object} obj
		 */
		step(obj, config = {}) {
			if (!this.animation) return
			for (let i in obj) {
				try {
					if (typeof obj[i] === 'object') {
						this.animation[i](...obj[i])
					} else {
						this.animation[i](obj[i])
					}
				} catch (e) {
					console.error(`方法 ${i} 不存在`)
				}
			}
			this.animation.step(config)
			return this
		},
		/**
		 *  ref 触发 执行动画
		 */
		run(fn) {
			if (!this.animation) return
			this.animation.run(fn)
		},
		// 开始过度动画
		open() {
			clearTimeout(this.timer)
			this.transform = ''
			this.isShow = true
			let { opacity, transform } = this.styleInit(false)
			if (typeof opacity !== 'undefined') {
				this.opacity = opacity
			}
			this.transform = transform
			// 确保动态样式已经生效后，执行动画，如果不加 nextTick ，会导致 wx 动画执行异常
			this.$nextTick(() => {
				// TODO 定时器保证动画完全执行，目前有些问题，后面会取消定时器
				this.timer = setTimeout(() => {
					this.animation = createAnimation(this.config, this)
					this.tranfromInit(false).step()
					this.animation.run()
					this.$emit('change', {
						detail: this.isShow
					})
				}, 20)
			})
		},
		// 关闭过度动画
		close(type) {
			if (!this.animation) return
			this.tranfromInit(true)
				.step()
				.run(() => {
					this.isShow = false
					this.animationData = null
					this.animation = null
					let { opacity, transform } = this.styleInit(false)
					this.opacity = opacity || 1
					this.transform = transform
					this.$emit('change', {
						detail: this.isShow
					})
				})
		},
		// 处理动画开始前的默认样式
		styleInit(type) {
			let customStyle = {
				transform: ''
			}
			let buildStyle = (type, mode) => {
				if (mode === 'fade') {
					customStyle.opacity = this.animationType(type)[mode]
				} else {
					customStyle.transform += this.animationType(type)[mode] + ' '
				}
			}
			if (typeof this.modeClass === 'string') {
				buildStyle(type, this.modeClass)
			} else {
				this.modeClass.forEach(mode => {
					buildStyle(type, mode)
				})
			}
			return customStyle
		},
		// 处理内置组合动画
		tranfromInit(type) {
			let buildTranfrom = (type, mode) => {
				let aniNum = null
				if (mode === 'fade') {
					aniNum = type ? 0 : 1
				} else {
					aniNum = type ? '-100%' : '0'
					if (mode === 'zoom-in') {
						aniNum = type ? 0.8 : 1
					}
					if (mode === 'zoom-out') {
						aniNum = type ? 1.2 : 1
					}
					if (mode === 'slide-right') {
						aniNum = type ? '100%' : '0'
					}
					if (mode === 'slide-bottom') {
						aniNum = type ? '100%' : '0'
					}
				}
				this.animation[this.animationMode()[mode]](aniNum)
			}
			if (typeof this.modeClass === 'string') {
				buildTranfrom(type, this.modeClass)
			} else {
				this.modeClass.forEach(mode => {
					buildTranfrom(type, mode)
				})
			}

			return this.animation
		},
		animationType(type) {
			return {
				fade: type ? 0 : 1,
				'slide-top': `translateY(${type ? '0' : '-100%'})`,
				'slide-right': `translateX(${type ? '0' : '100%'})`,
				'slide-bottom': `translateY(${type ? '0' : '100%'})`,
				'slide-left': `translateX(${type ? '0' : '-100%'})`,
				'zoom-in': `scaleX(${type ? 1 : 0.8}) scaleY(${type ? 1 : 0.8}) translate3d(-50%, -50%, 0)`,
				'zoom-out': `scaleX(${type ? 1 : 1.2}) scaleY(${type ? 1 : 1.2})`
			}
		},
		// 内置动画类型与实际动画对应字典
		animationMode() {
			return {
				fade: 'opacity',
				'slide-top': 'translateY',
				'slide-right': 'translateX',
				'slide-bottom': 'translateY',
				'slide-left': 'translateX',
				'zoom-in': 'scale',
				'zoom-out': 'scale'
			}
		},
		// 驼峰转中横线
		toLine(name) {
			return name.replace(/([A-Z])/g, '-$1').toLowerCase()
		}
	}
}
</script>

<style lang="scss">
</style>