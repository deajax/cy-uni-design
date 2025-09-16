<template>
	<view
		class="cy-goods-item--wrapper"
		:class="bordered ? '' : 'cy-goods-item--borderless'"
	>
		<view
			:class="[
				'cy-goods-item',
				`cy-goods-item--${layout}`,
				round ? 'cy-goods-item--round' : '',
				setClass,
				customClass,
			]"
			:hover-class="{ 'cy-goods-item--hover': hover }"
			:hover-stay-time="70"
			@click="handleTap"
		>
			<view class="cy-goods-item__prefix" v-if="layout === 'horizontal'">
				<slot name="prefix" />
			</view>
			<view :class="['cy-goods-item__image', customClassImage]">
				<view class="cy-goods-item__sellout" v-if="sellout">{{ sellout }}</view>
				<slot name="image" />
				<image
					class="cy-goods-item__image-image"
					:src="image"
					:mode="imageMode"
				/>
			</view>
			<view :class="['cy-goods-item__content', customClassContent]">
				<view class="cy-goods-item__content--main">
					<view :class="['cy-goods-item__content--title', customClassTitle]">
						<text
							class="cy-goods-item__content--title-text"
							v-if="titlePrefix"
							>{{ titlePrefix }}</text
						>
						<text
							class="cy-goods-item__content--title-text"
							:class="ellipsis ? 'cy-ellipsis-1' : 'cy-ellipsis-2'"
							>{{ title }}</text
						>
						<view
							v-if="description"
							:class="[
								'cy-goods-item__content--description',
								customClassDescription,
							]"
						>
							{{ description }}
						</view>
						<slot name="title" />
						<slot name="description" />
					</view>
					<slot />
				</view>
				<view :class="['cy-goods-item__content--note', customClassNote]">
					<view>
						<view
							:class="[
								'cy-goods-item__origin-price',
								customClassOriginPrice,
							]"
						>
							<template v-if="originPrice"> ¥{{ originPrice }} </template>
							<slot name="originPrice" />
						</view>
						<view :class="['cy-goods-item__price', customClassPrice]">
							<cy-price
								v-if="!isEmpty(price)"
								:value="price"
								theme="primary"
								:size="size"
								custom-class="cy-goods-item--price"
							/>
							<text
								:class="[
									'cy-goods-item__price--unit',
									customClassPriceUnit,
								]"
								v-if="unit"
								>{{ unit }}</text
							>
							<slot name="price" />
						</view>
					</view>
					<view :class="['cy-goods-item__action', customClassAction]">
						<slot name="action" />
					</view>
				</view>
				<slot name="extra" />
			</view>
			<slot name="right" />
		</view>
		<slot name="footer" />
	</view>
</template>

<script>
	export default {
		name: "goods-item",
		externalClasses: [
			"custom-class",
			"custom-class-image",
			"custom-class-content",
			"custom-class-title",
			"custom-class-description",
			"custom-class-note",
			"custom-class-price",
			"custom-class-price-unit",
			"custom-class-origin-price",
			"custom-class-action",
		],
		options: {
			styleIsolation: "shared",
			addGlobalClass: true,
			virtualHost: true,
			externalClasses: true,
		},
		props: {
			layout: {
				type: String,
				default: "horizontal", //vertical
			},
			size: {
				type: String,
				default: "medium", //small
			},
			image: String,
			imageMode: {
				type: String,
				default: "aspectFill",
			},
			title: String,
			titlePrefix: String,
			description: String,
			price: [String, Number],
			originPrice: [String, Number],
			unit: String,
			round: {
				type: Boolean,
				default: true,
			},
			hover: {
				type: Boolean,
				default: true,
			},
			bordered: {
				type: Boolean,
				default: true,
			},
			sellout: {
				type: [Boolean, String],
				default: false,
			},
			ellipsis: {
				type: Boolean,
				default: false,
			},
			url: String,
			jumpType: {
				type: String,
				default: "navigateTo",
			},
			disabled: {
				type: Boolean,
				default: false,
			},

			// externalClasses
			customClass: {
				type: [String, Array, Object],
				default: "",
			},
			customClassImage: {
				type: [String, Array, Object],
				default: "",
			},
			customClassContent: {
				type: [String, Array, Object],
				default: "",
			},
			customClassTitle: {
				type: [String, Array, Object],
				default: "",
			},
			customClassDescription: {
				type: [String, Array, Object],
				default: "",
			},
			customClassNote: {
				type: [String, Array, Object],
				default: "",
			},
			customClassPrice: {
				type: [String, Array, Object],
				default: "",
			},
			customClassPriceUnit: {
				type: [String, Array, Object],
				default: "",
			},
			customClassOriginPrice: {
				type: [String, Array, Object],
				default: "",
			},
			customClassAction: {
				type: [String, Array, Object],
				default: "",
			},
		},
		data() {
			return {};
		},
		computed: {
			setClass() {
				if (this.size == "small" && this.layout == "vertical") {
					return "cy-goods-item--small";
				}
			},
		},
		methods: {
			type: (para) => Object.prototype.toString.call(para).slice(8, -1),
			isEmpty(data) {
				//null,undefined,'',"",{},[],[{}] 匹配到这些值时，都是返回true
				if (
					data === "" ||
					data === "" ||
					data === "undefined" ||
					data === undefined ||
					data === null
				) {
					return true;
				} else if (
					JSON.stringify(data) === "{}" ||
					JSON.stringify(data) === "[]" ||
					JSON.stringify(data) === "[{}]"
				) {
					return true;
				}
				return false;
			},
			handleTap(event) {
				if (this.disabled) return;

				this.$emit("click", event);
				this.stop && this.preventEvent(event);
				if (!this.url) return;
				if (this.jumpType == "navigateTo") {
					uni.navigateTo({
						url: this.url,
					});
				} else if (this.jumpType == "switchTab") {
					uni.switchTab({
						url: this.url,
					});
				} else if (this.jumpType == "reLaunch") {
					uni.reLaunch({
						url: this.url,
					});
				} else if (this.jumpType == "redirectTo") {
					uni.redirectTo({
						url: this.url,
					});
				} else {
					uni.navigateTo({
						url: this.url,
					});
				}
			},
		},
		watch: {},

		// 组件周期函数--监听组件挂载完毕
		mounted() {},
		// 组件周期函数--监听组件数据更新之前
		beforeUpdate() {},
		// 组件周期函数--监听组件数据更新之后
		updated() {},
		// 组件周期函数--监听组件激活(显示)
		activated() {},
		// 组件周期函数--监听组件停用(隐藏)
		deactivated() {},
		// 组件周期函数--监听组件销毁之前
		beforeDestroy() {},
	};
</script>

<style lang="scss">
	@import "./goods-item.scss";
</style>
