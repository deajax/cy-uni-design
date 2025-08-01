<template>
    <view :class="['cy-cell', customClass, setClass, `cy-cell--${align}`]"
          :hover-class="!disabled && hover ? 'cy-cell--hover' : ''"
          @click="handleTap">
        <view class="cy-cell__left"
              :class="customClassLeft"
              v-if="leftIcon || leftIcon.name || $slots['left-icon'] || image || $slots.image">
            <cy-icon :name="leftIcon.name || leftIcon"
                     :size="leftIcon.size || ''"
                     :color="leftIcon.color || ''"
                     custom-class="cy-cell__left-icon" v-if="leftIcon" @click="onleftIconClick" />
            <slot name="left-icon"></slot>
            <image :src="image" mode="scaleToFill" :class="['cy-cell__left-image', customClassImage]" v-if="image" />
            <slot name="image" />
        </view>
        <view class="cy-cell__title" :class="customClassTitle" v-if="title || description || $slots.title || $slots.description">
            <view class="cy-cell__title-text" :class="customClassTitleText" v-if="title || $slots.title">
                <template v-if="title">{{ title }}</template>
                <slot name="title"></slot>
                <cy-icon v-if="required"
                         name="asterisk"
                         size="20"
                         color="var(--cell-required-color, #ef4444)"
                         :custom-style="{ marginLeft: '8rpx' }" />
            </view>
            <view class="cy-cell__description"
                  :class="customClassDescription"
                  v-if="description || $slots.description">
                <view class="cy-cell__description-text" :class="customClassDescriptionText">
                    <template v-if="description">{{ description }}</template>
                    <slot name="description"></slot>
                </view>
            </view>
            <slot name="extra"></slot>
        </view>
        <view class="cy-cell__note" :class="customClassNote" v-if="note || $slots.note">
            <template v-if="note">{{ note }}</template>
            <slot name="note"></slot>
            <slot></slot>
        </view>
        <view class="cy-cell__right" :class="customClassRight" v-if="arrow || rightIcon || $slots['right-icon']">
            <cy-icon :name="rightIcon || 'arrow-right-s-line'" custom-class="cy-cell__right-icon" v-if="arrow || rightIcon" @click="onRightIconClick" />
            <slot name="right-icon"></slot>
        </view>
    </view>
</template>

<script>
export default {
    name: 'Cell',
    externalClasses: ['custom-class', 'custom-class-title', 'custom-class-title-text', 'custom-class-description', 'custom-class-description-text', 'custom-class-note', 'custom-class-left', 'custom-class-image', 'custom-class-right'],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        // props
        bordered: {
            type: Boolean,
            default: true
        },
        forceBordered: {
            type: Boolean,
            default: false
        },
        required: Boolean,
        arrow: Boolean,
        hover: Boolean,
        leftIcon: [String, Object],
        rightIcon: String,
        image: String,
        title: {
            type: [String, Number],
            default: ''
        },
        description: [String, Number],
        note: [String, Number],
        align: {
            type: [String, Number],
            default: 'middle'
        },
        jumpType: String,
        url: String,

        // externalClasses
        customClass: {
			type: [String, Array],
			default: ''
		},
        customClassLeft: {
			type: [String, Array],
			default: ''
		},
        customClassImage: {
			type: [String, Array],
			default: ''
		},
        customClassTitle: {
			type: [String, Array],
			default: ''
		},
        customClassTitleText: {
			type: [String, Array],
			default: ''
		},
        customClassDescription: {
			type: [String, Array],
			default: ''
		},
        customClassDescriptionText: {
			type: [String, Array],
			default: ''
		},
        customClassNote: {
			type: [String, Array],
			default: ''
		},
        customClassRight: {
			type: [String, Array],
			default: ''
		},
    },
    data() {
        return {}
    },
    methods: {
        handleTap(event) {
            if (this.disabled) return;
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
        onleftIconClick(e) {
            this.$emit('left-icon-click', e);
        },
        onRightIconClick(e) {
            this.$emit('right-icon-click', e);
        },
    },
    computed: {
        setClass() {
            if (!this.bordered) {
                return 'cy-cell--borderless'
            }
            if (this.forceBordered) {
                return 'cy-cell--force-border'
            }
        },
    }
}
</script>

<style lang="scss">
@import './cell.scss';
</style>