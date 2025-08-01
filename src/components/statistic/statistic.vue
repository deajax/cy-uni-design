<template>
    <view :class="['cy-statistic', `cy-statistic--${align}`, customClass]">
        <view :class="['cy-statistic__title', customClassTitle]">
            {{ title }}
            <slot name="title" />
        </view>
        <view :class="['cy-statistic__content', customClassContent]">
            <text :class="['cy-statistic__content-prefix', customClassPrefix]">
                {{ prefix }}
                <slot name="prefix" />
            </text>
            <text :class="['cy-statistic__content-value', customClassValue]">
                {{ value }}
                <slot name="value" />
            </text>
            <text :class="['cy-statistic__content-suffix', customClassSuffix]">
                {{ suffix }}
                <slot name="suffix" />
            </text>
            <slot />
        </view>
    </view>
</template>

<script>
export default {
    name: 'statistic',
    externalClasses: [
        'custom-class',
        'custom-class-title',
        'custom-class-content',
        'custom-class-prefix',
        'custom-class-value',
        'custom-class-suffix'
    ],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        title: {
            type: String,
            default: ''
        },
        prefix: {
            type: String,
            default: ''
        },
        value: {
            type: [String, Number],
            default: ''
        },
        suffix: {
            type: String,
            default: ''
        },
        align: {
            type: String,
            default: 'center'
        },
        
        // externalClasses
        customClass: {
			type: [String, Array],
			default: ''
		},
        customClassTitle: {
			type: [String, Array],
			default: ''
		},
        customClassContent: {
			type: [String, Array],
			default: ''
		},
        customClassPrefix: {
			type: [String, Array],
			default: ''
		},
        customClassValue: {
			type: [String, Array],
			default: ''
		},
        customClassSuffix: {
			type: [String, Array],
			default: ''
		},
    },
};
</script>

<style lang="scss">
@import './statistic.scss';
</style>
