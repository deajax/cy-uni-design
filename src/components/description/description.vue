<template>
    <view :class="['cy-description', `cy-description--${size}`, customClass]" :style="customStyle" @click="handleTap">
        <view :class="['cy-description__icon', customClassIcon]" v-if="icon || $slots.icon">
            <cy-icon :name="icon.name || icon" :size="icon.size || ''" :color="icon.color || ''" />
            <slot name="icon"></slot>
        </view>
        <view :class="['cy-description__label', customClassLabel]" :style="customStyleLabel" v-if="label || $slots.label">
            <template v-if="label">{{ label }}：</template>
            <slot name="label"></slot>
        </view>
        <view :class="['cy-description__content', customClassContent]">
            <template v-if="content">{{ content }}</template>
            <slot name="content"></slot>
            <slot name="default"></slot>
            <slot></slot>
        </view>
        <slot name="extra"></slot>
    </view>
</template>

<script>
export default {
    name: 'description',
    externalClasses: ['custom-class', 'custom-class-label', 'custom-class-content'],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        icon: [String, Object],
        label: null,
        content: null,
        size: {
            type: String,
            default: 'middle'
        },
        jumpType: String,
        url: String,

        // externalClasses
        customClass: {
            type: [String, Array],
            default: ''
        },
        customClassIcon: {
            type: [String, Array],
            default: ''
        },
        customClassLabel: {
            type: [String, Array],
            default: ''
        },
        customClassContent: {
            type: [String, Array],
            default: ''
        },
        // externalStyles
        customStyle: {
            type: [String, Object],
            default: ''
        },
        customStyleLabel: {
            type: [String, Object],
            default: ''
        }
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
    }
};
</script>

<style lang="scss">
@import './description.scss';
</style>
