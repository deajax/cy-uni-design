<template>
    <view
          :class="['cy-tab-bar-item', split ? 'cy-tab-bar-item--split' : '', icon ? '' : 'cy-tab-bar-item--text-only', customClass]">
        <view :class="['cy-tab-bar-item__content', isChecked ? 'cy-tab-bar-item__content--checked' : '']"
              hover-class="cy-tab-bar-item__content--active" @click="handleTap">
            <view :class="['cy-tab-bar-item__icon', customClassImage]">
                <cy-badge v-if="badgeProps.dot || badgeProps.count"
                          :dot="badgeProps.dot || ''"
                          :count="badgeProps.count || ''"
                          :color="badgeProps.color || ''">
                    <cy-icon :name="icon" :size="iconOnly ? 56 : 48" />
                    <template #badge>
                        <slot name="badge" />
                    </template>
                </cy-badge>
                <cy-icon v-else-if="!!icon" :name="icon" :size="iconOnly ? 56 : 48" />
                <slot name="icon" />
            </view>
            <view class="cy-tab-bar-item__text">
                {{ text }}
                <slot />
            </view>
        </view>
    </view>
</template>

<script>
export default {
    name: 'cy-tab-bar-item',
    externalClasses: ['custom-class'],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    data() {
        return {
            isChecked: false,
            parentData: {
                value: null,
            }
        }
    },
    props: {
        /** 透传至 Badge 属性 */
        badgeProps: {
            type: Object,
            default: null,
        },
        /** 图标名称 */
        icon: {
            type: null,
        },
        /** 文本，自定义标题节点 */
        text: {
            type: String,
        },
        /** 点击后的跳转链接 */
        url: {
            type: String,
            default: '',
        },

        // externalClasses
        customClass: {
			type: [String, Array],
			default: ''
		},
    },
    created() {
        this.init()
    },
    methods: {
        init() {
            // 支付宝小程序不支持provide/inject，所以使用这个方法获取整个父组件，在created定义，避免循环引用
            this.updateParentData()
            if (!this.parent) {
                console.log('tab-bar-item必须搭配tab-bar组件使用');
            }
            // 本子组件在u-tabbar的children数组中的索引
            const index = this.parent.children.indexOf(this)
            // 判断本组件的name(如果没有定义name，就用index索引)是否等于父组件的value参数
            this.isChecked = (this.name || index) === this.parentData.value
        },
        updateParentData() {
            // 此方法在mixin中
            this.getParentData('cy-tab-bar')
        },
        // 此方法将会被父组件u-tabbar调用
        updateFromParent() {
            // 重新初始化
            this.init()
        },
        handleTap() {
            this.$nextTick(() => {
                const index = this.parent.children.indexOf(this)
                const name = this.name || index
                // 点击的item为非激活的item才发出change事件
                if (name !== this.parent.value) {
                    this.parent.$emit('change', name)
                }
                this.$emit('click', name)
            })
        },
    },
};
</script>

<style lang="scss">
@import './tab-bar-item.scss';
</style>