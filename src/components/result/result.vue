<template>
    <view :class="['cy-result', `cy-result--${status}`, customClass]">
        <view :class="['cy-result--icon', customClassIcon]">
            <template v-if="status == 'success'">
                <cy-icon name="checkbox-circle-fill" />
            </template>
            <template v-if="status == 'info'">
                <cy-icon name="information-fill" />
            </template>
            <template v-if="status == 'warning'">
                <cy-icon name="alert-fill" />
            </template>
            <template v-if="status == 'error'">
                <cy-icon name="close-circle-fill" />
            </template>
            <slot v-else name="icon" />
        </view>
        <view :class="['cy-result--title', customClassTitle]">
            <template v-if="title">
                {{ title }}
            </template>
            <slot name="title" />
        </view>
        <slot />
        <view :class="['cy-result--description', customClassDescription]">
            <template v-if="description">
                {{ description }}
            </template>
            <slot name="description" />
        </view>
        <view :class="['cy-result--extra', customClassExtra]" v-if="$slots.extra">
            <slot name="extra" />
        </view>
    </view>
</template>

<script>
export default {
    name: "result",
    externalClasses: ['custom-class','custom-class-icon','custom-class-title','custom-class-description','custom-class-extra'],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        title: {
            type: String
        },
        description: {
            type: String
        },
        status: {
            type: String
        },

        // externalClasses
        customClass: {
            type: [String, Array],
            default: ''
        },
        customClassIcon: {
            type: [String, Array],
            default: ''
        },
        customClassTitle: {
            type: [String, Array],
            default: ''
        },
        customClassDescription: {
            type: [String, Array],
            default: ''
        },
        customClassExtra: {
            type: [String, Array],
            default: ''
        },
    },
    data() {
        return {}
    },
} 
</script>

<style lang="scss">
@import './result.scss';
</style>