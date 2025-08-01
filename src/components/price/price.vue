<template>
    <view :class="['cy-price', customClass, `cy-price--${theme}`, `cy-price--${size}`]" @click="handleTap">
        <view :class="['cy-price__prefix-icon', customClassPrefixIcon]">
            <slot name="prefix-icon" />
            <view class="cy-price__cny-icon" v-if="showSymbol"></view>
        </view>
        <view :class="['cy-price__content', customClassContent]">
            {{ value }}
            <slot />
        </view>
        <view
            :class="['cy-price__suffix-icon', customClassSuffixIcon]"
            v-if="$slots['suffix-icon']"
        >
            <slot name="suffix-icon" />
        </view>
    </view>
</template>

<script>
export default {
    name: 'price',
    externalClasses: [
        'custom-class',
        'custom-class-content',
        'custom-class-prefix-icon',
        'custom-class-suffix-icon'
    ],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        value: [String, Number],
        theme: {
            type: String,
            default: 'default'
        },
        size: {
            type: String,
            default: 'medium'
        },
        showSymbol: {
            type: Boolean,
            default: true
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
        customClassPrefixIcon: {
			type: [String, Array],
			default: ''
		},
        customClassSuffixIcon: {
			type: [String, Array],
			default: ''
		},
    },
    data() {
        return {};
    },
    methods: {
        handleTap(event) {
            this.$emit('click', event);
        }
    },
    computed: {}
};
</script>

<style lang="scss">
@import './price.scss';
</style>
