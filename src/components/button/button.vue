<template>
	<button :id="id"
			:class="[
				customClass,
				setClass,
				disabled ? 'cy-button--disabled' : '',
				`cy-button--${theme}`,
				`cy-button--${shape}`,
				`cy-button--${variant}`,
				`cy-button--size-${size}`,
				'cy-button'
			]"
			:form-type="formType"
			:open-type="disabled || loading ? '' : openType"
			:hover-class="disabled || loading ? '' : (hoverClass || 'cy-button--hover')"
			:hover-stop-propagation="hoverStopPropagation"
			:hover-start-time="hoverStartTime"
			:hover-stay-time="hoverStayTime"
			:lang="lang"
			:session-from="sessionFrom"
			:send-message-title="sendMessageTitle"
			:send-message-path="sendMessagePath"
			:send-message-img="sendMessageImg"
			:app-parameter="appParameter"
			:show-message-card="showMessageCard"
			@click="handleTap"
			@getuserinfo="handleGetuserinfo"
			@contact="handleContact"
			@getphonenumber="handleGetphonenumber"
			@error="handleError"
			@opensetting="handleOpensetting"
			@launchapp="handleLaunchapp"
			@chooseavatar="handleChooseavatar"
			@agreeprivacyauthorization="handleAgreeprivacyauthorization">
		<cy-loading v-if="loading" color="currentColor" custom-class="cy-button__icon cy-button__loading" />
		<!-- #ifdef MP-ALIPAY -->
		<cy-icon v-if="icon || icon.name" :name="icon.name || icon" :size="icon.size || ''" :color="icon.color || ''"
			custom-class="cy-button__icon" />
		<!-- #endif -->
		<!-- #ifndef MP-ALIPAY -->
		<cy-icon v-if="icon || icon.name" :name="icon.name || icon" :size="icon.size || ''" :color="icon.color || ''"
			:custom-class="'cy-button__icon ' + customClassIcon" />
		<!-- #endif -->
		<view class="cy-button__content" :class="customClassContent">
			<slot name="content" />
			<template>{{ content }}</template>
			<slot />
		</view>
		<slot name="suffix" />
	</button>
</template>

<script>
export default {
	name: 'Button',
	externalClasses: ['custom-class', 'custom-class-icon', 'custom-class-content'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		id: {
			type: String,
			default: ''
		},
		block: {
			type: Boolean,
			default: false
		},
		content: {
			type: String,
			default: ''
		},
		disabled: {
			type: Boolean,
			default: false
		},
		ghost: {
			type: Boolean,
			default: false
		},
		icon: {
			type: [String, Object],
			default: ''
		},
		loading: {
			type: Boolean,
			default: false
		},
		shape: {
			type: String,
			default: 'rectangle'
		},
		size: {
			type: String,
			default: 'medium'
		},
		theme: {
			type: String,
			default: 'default'
		},
		variant: {
			type: String,
			default: 'base'
		},
		formType: {
			type: String,
			default: ''
		},
		openType: {
			type: String,
			default: ''
		},
		hoverClass: {
			type: String,
			default: ''
		},
		hoverStopPropagation: {
			type: Boolean,
			default: false
		},
		hoverStartTime: {
			type: Number,
			default: 20,
		},
		hoverStayTime: {
			type: Number,
			default: 70,
		},
		lang: {
			type: String,
			default: 'en',
		},
		sessionFrom: {
			type: String,
			default: ''
		},
		sendMessageTitle: {
			type: String,
			default: ''
		},
		sendMessagePath: {
			type: String,
			default: ''
		},
		sendMessageImg: {
			type: String,
			default: ''
		},
		appParameter: {
			type: String,
			default: ''
		},
		showMessageCard: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassIcon: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
	},
	methods: {
		handleTap(event) {
			if (this.disabled || this.loading) return;
			this.$emit('click', event);
			if (this.stop) this.preventEvent(event);
		},
		handleGetuserinfo(event) {
			this.$emit("getuserinfo", event);
		},
		handleContact(event) {
			this.$emit("contact", event);
		},
		handleGetphonenumber(event) {
			this.$emit("getphonenumber", event);
		},
		handleError(event) {
			this.$emit("error", event);
		},
		handleOpensetting(event) {
			this.$emit("opensetting", event);
		},
		handleLaunchapp(event) {
			this.$emit("launchapp", event);
		},
		handleChooseavatar(event) {
			this.$emit("chooseavatar", event);
		},
		handleAgreeprivacyauthorization(event) {
			this.$emit("agreeprivacyauthorization", event);
		},
		preventEvent(event) {
			if (this.stop) {
				event.stopPropagation();
				event.preventDefault();
			}
		}
	},
	computed: {
		setClass() {
			if (this.block) {
				return 'cy-button--block';
			}
			if (this.disabled) {
				return 'cy-button--disabled';
			}
			if (this.ghost) {
				return 'cy-button--ghost';
			}
			return '';
		},
	}
}
</script>

<style lang="scss">
@import './button.scss'
</style>
