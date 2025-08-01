<template>
    <view
        :class="['cy-gap', `cy-gap--${layout}`, wrap ? 'cy-gap--wrap' : 'cy-gap--nowrap', customClass]"
        :style="[
            columnGap ? { columnGap: columnGap + 'px' } : '',
            rowGap ? { rowGap: rowGap + 'px' } : ''
        ]"
    >
        <slot />
    </view>
</template>

<script>
export default {
    name: 'gap',
    externalClasses: ['custom-class'],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        layout: {
            type: String,
            default: 'horizontal'
        },
        gutter: {
            type: [Array, String],
            default: 4
        },
        wrap: {
            type: Boolean,
            default: true
        },

        // externalClasses
        customClass: {
			type: [String, Array],
			default: ''
		},
    },
    data() {
        return {
            columnGap: '',
            rowGap: ''
        };
    },
    created() {
        this.setGutterField();
    },
    computed: {},
    methods: {
        setGutterField() {
            if (this.layout == 'vertical') {
                this.rowGap = this.gutter;
            } else {
                if (this.gutter.length > 0) {
                    this.columnGap = this.gutter[0];
                    this.rowGap = this.gutter[1];
                }
            }
        }
    },
    watch: {},

    // 组件周期函数--监听组件挂载完毕
    mounted() {},
    // 组件周期函数--监听组件数据更新之前
    beforeUpdate() {},
    // 组件周期函数--监听组件数据更新之后
    updated() {},
    // 组件周期函数--监听组件激活(显示)
    activated() {},
    // 组件周期函数--监听组件停用(隐藏)
    deactivated() {},
    // 组件周期函数--监听组件销毁之前
    beforeDestroy() {}
};
</script>

<style lang="scss">
@import './gap.scss';
</style>
