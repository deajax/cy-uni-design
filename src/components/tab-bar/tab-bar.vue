<template>
    <view class="cy-tab-bar--wrapper">
        <view
              :style="{ zIndex: zIndex }"
              :class="[
                'cy-tab-bar',
                bordered ? 'cy-tab-bar--border' : '',
                fixed ? 'cy-tab-bar--fixed' : '',
                safeAreaInsetBottom ? 'cy-tab-bar--safe' : '',
                customClass
            ]">
            <slot />
        </view>
        <view v-if="placeholder" class="cy-tab-bar--placeholder"></view>
    </view>
</template>

<script>
export default {
    name: 'cy-tab-bar',
    externalClasses: ['custom-class'],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        value: {
            type: [String, Number, null],
        },
        bordered: {
            type: Boolean,
            default: true
        },
        fixed: {
            type: Boolean,
            default: true
        },
        safeAreaInsetBottom: {
            type: Boolean,
            default: true
        },
        placeholder: {
            type: Boolean,
            default: true
        },
        zIndex: {
            type: [String, Number],
            default: 100
        },

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
        // 监听多个参数的变化，通过在computed执行对应的操作
        updateChild() {
            return [this.value]
        },
        updatePlaceholder() {
            return [this.fixed, this.placeholder]
        }
    },
    watch: {
        updateChild() {
            // 如果updateChildren中的元素发生了变化，则执行子元素初始化操作
            this.updateChildren()
        },
    },
    created() {
        this.children = []
    },
    methods: {
        updateChildren() {
            // 如果存在子元素，则执行子元素的updateFromParent进行更新数据
            this.children.length && this.children.map(child => child.updateFromParent())
        },
    }
};
</script>

<style lang="scss">
@import './tab-bar.scss';
</style>
