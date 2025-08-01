<template>
	<view :class="['cy-goods-action', customClass]">
		<view class="cy-goods-action--fixed"
			  :style="[safeAreaInsetBottom ? statusBarBottom == 0 ? { paddingBottom: '16px' } : { paddingBottom: statusBarBottom + 'px' } : '']">
			<view :class="['cy-goods-action__content', customClassContent]">
				<slot name="content" />
				<view :class="['cy-goods-action__content-icon', customClassIcon]" v-if="$slots.default">
					<slot />
				</view>
				<view :class="['cy-goods-action__content-button', customClassAction]">
					<cy-button v-if="addCartBtn" theme="light" shape="round" block
							   @click="handleAddCart">{{ addCartBtnText }}</cy-button>
					<cy-button v-if="buyNowBtn" theme="primary" shape="round" block
							   @click="handleBuyNow">{{ buyNowBtnText }}</cy-button>
					<slot name="action" />
				</view>
			</view>
		</view>
		<view class="cy-goods-action__placeholder"></view>
	</view>
</template>

<script>
export default {
	name: "goods-action",
	externalClasses: ['custom-class', 'custom-class-content', 'custom-class-icon', 'custom-class-action'],
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
		addCartBtn: {
			type: Boolean,
			default: true
		},
		buyNowBtn: {
			type: Boolean,
			default: true
		},
        addCartBtnText: {
            type: String,
            default: '加入购物车'
        },
        buyNowBtnText: {
            type: String,
            default: '立即购买'
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
		customClassIcon: {
			type: [String, Array],
			default: ''
		},
		customClassAction: {
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
		handleAddCart(event) {
			this.$emit('add-cart', event);
		},
		handleBuyNow(event) {
			this.$emit('buy-now', event);
		}
	},
	onReady() {
		console.log(uni.getWindowInfo());
		// #ifdef MP-ALIPAY
		this.statusBarBottom = uni.getWindowInfo().screenHeight - uni.getWindowInfo().safeArea.height - uni.getWindowInfo().statusBarHeight
		// #endif
		// #ifndef MP-ALIPAY
		this.statusBarBottom = uni.getWindowInfo().safeAreaInsets.bottom
		// #endif
	},
} 
</script>

<style lang="scss">
@import './goods-action.scss';
</style>