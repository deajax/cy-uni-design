<template>
	<view :class="['cy-submit-bar', customClass]">
		<view class="cy-submit-bar--fixed"
			:style="[safeAreaInsetBottom ? statusBarBottom == 0 ? { paddingBottom: '16px' } : { paddingBottom: statusBarBottom + 'px' } : '', zIndex ? { zIndex: zIndex } : '']">
			<slot name="custom" v-if="$slots.custom" />
			<view :class="['cy-submit-bar__content', customClassContent]" v-else>
				<view :class="['cy-submit-bar__content-actions', customClassActions]">
					<view :class="['cy-submit-bar__content-left', customClassLeft]">
						<slot name="left" />
					</view>
					<view :class="['cy-submit-bar__content-currency', customClassCurrency]">
                        <view :class="['cy-submit-bar__content-price', customClassDescription]" v-if="$slots.price || price">
                            <slot name="price"></slot>
                            <cy-price :value="price" :custom-class="customClassPrice" />
                        </view>
						<view :class="['cy-submit-bar__content-description', customClassDescription]"
							v-if="$slots.description || description">
							{{ description }}
							<slot name="description" />
						</view>
					</view>
					<slot name="content" />
				</view>
				<view :class="['cy-submit-bar__content-button', customClassButton]">
					<cy-button
							custom-class="cy-submit-bar__content-button--primary"
							:theme="buttonProps.theme || 'primary'"
							:shape="buttonProps.shape || 'round'"
							:loading="buttonProps.loading || false"
							:disabled="disabled"
							block
							@click="handleTap"
							v-if="!$slots.button"
						>
						{{ buttonText }}
					</cy-button>
					<slot name="button" />
				</view>
			</view>
		</view>
		<view v-if="placeholder" class="cy-submit-bar__placeholder"></view>
	</view>
</template>

<script>
export default {
	name: "submit-bar",
	externalClasses: ['custom-class', 'custom-class-content', 'custom-class-actions', 'custom-class-left', 'custom-class-currency', 'custom-class-price', 'custom-class-description', 'custom-class-button'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		safeAreaInsetBottom: {
			type: Boolean,
			default: true,
		},
        placeholder: {
			type: Boolean,
			default: true,
		},
		price: {
			type: [Number, String, Boolean],
			default: '0',
		},
		buttonProps: {
			type: Object,
			default: () => ({}),
		},
		buttonText: {
			type: String,
			default: '提交订单',
		},
		description: {
			type: String,
			default: '',
		},
		zIndex: {
			type: [Number, String],
			default: '5001',
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
		customClassActions: {
			type: [String, Array],
			default: ''
		},
		customClassLeft: {
			type: [String, Array],
			default: ''
		},
		customClassCurrency: {
			type: [String, Array],
			default: ''
		},
		customClassPrice: {
			type: [String, Array],
			default: ''
		},
		customClassDescription: {
			type: [String, Array],
			default: ''
		},
		customClassButton: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			statusBarBottom: 0,
		}
	},
	computed: {},
	methods: {
		handleTap(e) {
			if (this.disabled) return;
			this.$emit('submit', e);
		}
	},
	onReady() {
		// #ifdef MP-ALIPAY
		this.statusBarBottom = uni.getWindowInfo().screenHeight - uni.getWindowInfo().safeArea.height - uni.getWindowInfo().statusBarHeight;
		// #endif
		// #ifndef MP-ALIPAY
		this.statusBarBottom = uni.getWindowInfo().safeAreaInsets.bottom
		// #endif
	},
} 
</script>

<style lang="scss">
@import './submit-bar.scss';
</style>