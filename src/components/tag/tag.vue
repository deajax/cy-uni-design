<template>
    <view
        :class="[
            'cy-tag',
            customClass,
            `cy-tag--${variant}`,
            `cy-tag--${theme}`,
            `cy-tag--${shape}`,
            `cy-tag--${size}`
        ]"
        :style="[maxWidth ? mWidth : '', background ? bgColor : '', color ? fontColor : '']"
        @click="handleTap"
    >
        <view :class="['cy-tag__icon', customClassIcon]" v-if="icon">
            <cy-icon :name="icon.name || icon" :size="icon.size || ''" :color="icon.color || ''" />
            <slot name="icon" />
        </view>
        <view :class="['cy-tag__text', ellipsis ? 'ellipsis' : '', customClassText]">
            {{ text }}
            <slot />
            </view>
        <cy-icon
            v-if="closable"
            name="close-line"
            :custom-class="['cy-tag__icon-close ' + customClassClosable]"
            @click="handleClose"
        />
        <slot v-else name="closable" />
    </view>
</template>

<script>
export default {
    name: 'tag',
    externalClasses: [
        'custom-class',
        'custom-class-icon',
        'custom-class-text',
        'custom-class-closable'
    ],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        icon: [String, Object],
        closable: Boolean,
        disabled: Boolean,
        shape: {
            type: String,
            default: 'square'
        },
        size: {
            type: String,
            default: 'medium'
        },
        theme: {
            type: String,
            default: 'default'
        },
        variant: {
            type: String,
            default: 'dark'
        },
        maxWidth: [String, Number],
        background: {
            type:String,
            default:''
        },
        color: {
            type:String,
            default:''
        },
        text: {
            type:String,
            default:''
        },
        ellipsis: {
            type:Boolean,
            default:true
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
        customClassText: {
			type: [String, Array],
			default: ''
		},
        customClassClosable: {
			type: [String, Array],
			default: ''
		},
    },
    data() {
        return {};
    },
    computed: {
        mWidth() {
            return {
                maxWidth: `${this.maxWidth}px`
            };
        },
        bgColor() {
            return {
                backgroundColor: this.background,
                borderColor: this.background
            };
        },
        fontColor() {
            return {
                color: this.color
            };
        }
    },
    methods: {
        handleTap(e) {
            this.$emit('click', e);
        },
        handleClose(e) {
            this.$emit('close', e);
        }
    }
};
</script>

<style lang="scss">
@import './tag.scss';
</style>
