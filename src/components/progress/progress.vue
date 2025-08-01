<template>
    <view :class="['cy-progress', `cy-progress--${status}`, customClass]">
        <view :class="['cy-progress__bar', customClassBar]"
              :style="{ height: `${strokeWidth}px`, borderRadius: `${radius}px`, background: background }">
            <view
                :class="['cy-progress__inner', customClassInner]"
                :style="{ width: `${percent}%`, background: activeColor }">
                <slot name="inner"></slot>
            </view>
        </view>
        <view class="cy-progress__content">{{ content }}</view>
        <slot name="content"></slot>
        <slot></slot>
    </view>
</template>

<script>
export default {
    name: 'progress',
    externalClasses: [],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        percent: {
            type: [Number, String]
        },
        content: {
            type: String
        },
        status: {
            type: String,
            default: 'primary' // success/error/warning/primary
        },
        strokeWidth: {
            type: [Number, String],
            default: 8
        },
        radius: {
            type: [Number, String],
            default: 0
        },
        background: {
            type: String
        },
        activeColor: {
            type: String
        }
    }
};
</script>

<style lang="scss">
@import './progress.scss';
</style>