<template>
    <view :class="['cy-icon', customClass]" :style="[color ? iconColor : '', size ? fontSize : '', customStyle]"
        @click="bindclick">
        <text class="cy-icon-base" :class="prefix ? prefix + ' ' + name : 'ri-' + name"></text>
        <slot />
    </view>
</template>

<script>
export default {
    name: 'Cell',
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    externalClasses: ['custom-class', 'custom-style'],
    props: {
        name: String,
        color: String,
        size: [String, Number],
        prefix: String,

        // externalClasses
        customClass: {
            type: [String, Array],
            default: ''
        },
        // externalStyles
        customStyle: {
            type: [String, Object],
            default: ''
        },
    },
    computed: {
        iconColor() {
            return {
                color: this.color
            }
        },
        fontSize() {
            return {
                fontSize: `${this.size}rpx`
            };
        },
    },
    methods: {
        bindclick(event) {
            this.$emit('click', event);
        }
    }
}
</script>

<style lang="scss">
@import './remixicon@4.6.0.scss';
@import './icon.scss';
</style>