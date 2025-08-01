<template>
	<view :class="['cy-grid-item', { 'cy-grid-item--auto-size': column == 0 }, customClass]"
		  :style="gridStyle"
		  :hover-class="hover ? 'cy-grid-item--hover' : ''"
		  hover-stay-time="70"
		  @click="handleTap">
		<view :class="[`cy-grid-item__wrapper cy-grid-item__wrapper--${layout}`]"
			  :style="gridStyleWrapper">
			<view :class="[`cy-grid-item__content cy-grid-item__content--${layout} cy-grid-item__content--${align}`, customClassContent]"
				  :style="gridStyleContent">
				<slot />
				<cy-badge :dot="badgeProps.dot || false"
						  :count="badgeProps.count || ''"
						  :color="badgeProps.color || ''">
					<view :class="['cy-grid-item__image-wrapper', customClassImageWrap]">
                        <view
                            v-if="image || imageProps.src || $slots.image"
                            :class="['cy-grid-item__image', customClassImage, getImageSize]"
                            :style="imageProps.size ? `width: ${imageProps.size}; height: ${imageProps.size}` : imageProps.radius ? `border-radius: ${imageProps.radius}` : ''"
                        >
                          <image
                               :class="['cy-grid__image']"
                               :src="image || imageProps.src"
                               :mode="imageProps.mode || 'aspectFill'" />
                          <slot name="image" />
                        </view>
						<cy-icon v-if="icon || icon.name"
								 :name="icon.name || icon"
								 :size="icon.size || ''"
								 :color="icon.color || ''"
								 custom-class="cy-grid-item__icon" />
						<slot name="icon" />
					</view>
					<template #badge>
						<slot name="badge" />
					</template>
				</cy-badge>
				<view :class="[`cy-grid-item__words cy-grid-item__words--${layout}`]">
					<view v-if="text" :class="[`cy-grid-item__text cy-grid-item__text--${layout}`, customClassText]">
						{{ text }}
					</view>
					<slot name="text" />
					<view v-if="description" :class="[`cy-grid-item__description cy-grid-item__description--${layout}`, customClassDescription]">
						{{ description }}
					</view>
					<slot name="description" />
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: "grid-item",
	externalClasses: ['custom-class', 'custom-class-content', 'custom-class-image-wrap', 'custom-class-image', 'custom-class-icon', 'custom-class-text', 'custom-class-description'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		/** 透传至 Badge 属性 */
		badgeProps: {
			type: Object,
			default: {},
		},
		/** 文本以外的更多描述，辅助信息。可以通过 Props 传入文本，也可以自定义标题节点 */
		description: {
			type: String,
		},
		/** 组件类名，分别用于设置组件外层元素、图片、文本、描述等元素类名 */
		externalClasses: {
			type: Array,
		},
		/** 图标名称。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon` */
		icon: {
			type: [String, Object, Array],
			default: ''
		},
		/** 图片，可以是图片地址，也可以自定义图片节点 */
		image: {
			type: String,
		},
		/** 透传至 Image 组件 */
		imageProps: {
			type: Object,
		},
		/** 链接跳转类型 */
		jumpType: {
			type: String,
			default: 'navigate-to',
		},
		/** 内容布局方式 */
		layout: {
			type: String,
			default: 'vertical',
		},
		/** 文本，可以通过 Props 传入文本，也可以自定义标题节点 */
		text: {
			type: String,
		},
		/** 点击后的跳转链接 */
		url: {
			type: String,
			default: '',
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
		customClassImageWrap: {
			type: [String, Array],
			default: ''
		},
		customClassImage: {
			type: [String, Array],
			default: ''
		},
		customClassIcon: {
			type: [String, Array],
			default: ''
		},
		customClassText: {
			type: [String, Array],
			default: ''
		},
		customClassDescription: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			column: 0,
			gutter: 0,
			align: 'center',
			bordered: false
		}
	},
	inject: ['grid'],
	computed: {
		gridStyle() {
			return this.column > 0 ? `width:${(1 / this.column) * 100}%` : '';
		},
		gridStyleContent() {
			return this.bordered ? 'border-top: 1px solid var(--cy-border-level-1-color, #F0F0F0); border-left: 1px solid var(--cy-border-level-1-color, #F0F0F0)' : '';
		},
		gridStyleWrapper() {
			return this.gutter ? `padding-left: ${this.gutter * 2}rpx; padding-top: ${this.gutter * 2}rpx;` : ''
		},

		getImageSize() {
			if (this.column >= 5) {
				return 'cy-grid-item__image--small'
			}
			if (this.column == 4) {
				return 'cy-grid-item__image--middle'
			}
			return 'cy-grid-item__image--large'
		},
	},
	created() {
		this.column = this.grid.column;
		this.gutter = this.grid.gutter;
		this.align = this.grid.align;
		this.bordered = this.grid.bordered;
	},
	methods: {
		handleTap(event) {
			this.$emit('click', event);
			this.stop && this.preventEvent(event);
			if (!this.url) return;
			if (this.jumpType == 'navigateTo') {
				uni.navigateTo({
					url: this.url
				});
			} else if (this.jumpType == 'switchTab') {
				uni.switchTab({
					url: this.url
				});
			} else if (this.jumpType == 'reLaunch') {
				uni.reLaunch({
					url: this.url
				});
			} else if (this.jumpType == 'redirectTo') {
				uni.redirectTo({
					url: this.url
				});
			} else {
				uni.navigateTo({
					url: this.url
				});
			}
		},
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
@import './grid-item.scss';
</style>