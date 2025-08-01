<template>
	<view
		  :class="['cy-message', `cy-message--${theme}`, fadeClass, customClass]"
		  :style="customStyle"
		  :animation="showAnimation"
		  :id="id || 'cy-message'"
		  aria-role="alert">
		<view class="cy-message__icon--left">
			<slot name="icon" />
			<cy-icon v-if="icon || icon.name" :name="icon.name || icon"
					 :size="icon.size || ''"
					 :color="icon.color || ''" />
			<cy-icon v-else
					 :name="theme == 'success' ? 'checkbox-circle-fill' : theme == 'error' ? 'error-warning-fill' : 'information-fill'" />
		</view>
		<view
			  :class="['cy-message__text-wrap', marquee ? 'cy-message__text-nowrap' : '']"
			  :style="{ 'text-align': align }"
			  id="cy-message__text-wrap">
			<view :class="['cy-message__text', customClassContent]" id="cy-message__text" :animation="animation">
				<template v-if="content">{{ content }}</template>
				<slot name="content" />
				<slot />
			</view>
		</view>

		<cy-text
				 v-if="link && link.content"
				 :custom-class="'cy-message__link ' + customClassLink"
				 :disabled="link.disabled || false"
				 :hover="link.hover || true"
				 :theme="link.theme || 'primary'"
				 :size="link.size || 'medium'"
				 :prefixIcon="link.prefixIcon || ''"
				 :suffixIcon="link.suffixIcon || ''"
				 :underline="link.underline || false"
				 :content="link.content || ''"
				 :navigatorProps="link.navigatorProps || null"
				 @complete="handleLinkClick" />
		<slot name="link" />
		<view class="cy-message__icon--right" @click="handleClose">
			<slot name="close-btn" />
			<cy-icon v-if="closeBtn"
					 name="close-line"
					 :custom-class="customClassCloseBtn" />
		</view>
	</view>
</template>

<script>
export default {
	name: "message",
	externalClasses: ['custom-class', 'custom-class-content', 'custom-class-link', 'custom-class-close-btn'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		/** 文本对齐方式 */
		align: {
			type: String,
			default: 'left',
		},
		/** 关闭按钮，可以自定义。值为 true 显示默认关闭按钮，值为 false 不显示关闭按钮。值类型为 string 则直接显示值，如：“关闭”。也可以完全自定义按钮 */
		closeBtn: {
			type: null,
			default: false,
		},
		/** 用于自定义消息弹出内容 */
		content: {
			type: String,
		},
		/** 消息内置计时器，计时到达时会触发 duration-end 事件。单位：毫秒。值为 0 则表示没有计时器。 */
		duration: {
			type: Number,
			default: 3000,
		},
		/** 消息提醒前面的图标。也可以完全自定义图标节点 */
		icon: {
			type: [String, Object],
			default: ''
		},
		/** 跑马灯效果。speed 指速度控制；loop 指循环播放次数，值为 -1 表示循环播放，值为 0 表示不循环播放；delay 表示延迟多久开始播放 */
		marquee: {
			type: null,
			default: false,
		},
		/** 相对于 placement 的偏移量，示例：[-10, 20] 或 ['10rpx', '8rpx'] */
		offset: {
			type: Array,
		},
		/** 消息组件风格 */
		theme: {
			type: String,
			default: 'info',
		},
		/** 链接名称。值为字符串表示链接名称，值为 `Object` 类型，表示透传至 `Link`。 */
		link: {
			type: null,
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
		customClassLink: {
			type: [String, Array],
			default: ''
		},
		customClassCloseBtn: {
			type: [String, Array],
			default: ''
		},
		// externalStyles
		customStyle: {
			type: [String, Object],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {},
	methods: {
		handleClose(event) {
			this.$emit('click', event);
		}
	},
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
@import './message.scss';
</style>