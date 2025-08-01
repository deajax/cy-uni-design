<template>
    <view class="cy-cell-group" :class="customClass">
        <view class="cy-cell-group__header" :class="customClassHeader">
            <view class="cy-cell-group__title" :class="customClassTitle">{{ title }}</view>
            <view class="cy-cell-group__extra" :class="customClassExtra">
                <slot name="extra" />
            </view>
            <slot name="header" />
        </view>
        <view
            class="cy-cell-group__content"
            :class="[customClassContent.toString().replace(/,/g,' '), borderClass, themeCard]"
            @click="handleTap"
        >
            <slot />
        </view>
    </view>
</template>

<script>
export default {
    name: 'CellGroup',
    externalClasses: [
        'custom-class',
        'custom-class-header',
        'custom-class-title',
        'custom-class-extra',
        'custom-class-content'
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
        theme: {
            type: String,
            default: ''
        },
        bordered: {
            type: Boolean,
            default: true
        },

        // externalClasses
        customClass: {
            type: [String, Array],
            default: ''
        },
        customClassHeader: {
            type: [String, Array],
            default: ''
        },
        customClassTitle: {
            type: [String, Array],
            default: ''
        },
        customClassExtra: {
            type: [String, Array],
            default: ''
        },
        customClassContent: {
            type: [String, Array],
            default: ''
        }
    },
    computed: {
        borderClass() {
            return this.bordered ? 'cy-cell-group--bordered' : '';
        },
        themeCard() {
            return this.theme == 'card' ? 'cy-cell-group--card' : '';
        }
    },
    methods: {
        handleTap(event) {
            this.$emit('click', event);
            this.stop && this.preventEvent(event);
        }
    }
};
</script>

<style lang="scss">
@import './cell-group.scss';
</style>
