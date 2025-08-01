<template>
    <cy-popup :ref="popupRef" type="center" :closeBtn="closeBtn" :closeOnOverlayClick="closeOnOverlayClick"
        @close="handleClose">
        <view :class="['cy-dialog ' + customClass]" slot="content">
            <slot name="top" />
            <view :class="['cy-dialog__content', customClassContent]">
                <view v-if="title" class="cy-dialog__header">{{ title }}</view>
                <slot name="title" />
                <view v-if="content || $slots.content" class="cy-dialog__body">
                    <text class="cy-dialog__body-text">{{ content }}</text>
                    <slot name="content" />
                </view>
                <slot name="middle" />
            </view>
            <slot name="default" />
            <slot />
            <view :class="[
                'cy-dialog__footer',
                buttonLayout === 'vertical' && 'cy-dialog__footer--column',
                customClassAction
            ]">
                <slot name="actions" />
                <template v-if="cancelBtn">
                    <cy-button block :custom-class="`cy-dialog__button--${buttonLayout} ` + customClassCancel"
                        :theme="cancelBtn.theme || 'light'" :content="cancelBtn.content || '取消'"
                        :variant="cancelBtn.variant || ''" :ghost="cancelBtn.ghost || ''" :icon="cancelBtn.icon || ''"
                        :loading="cancelBtn.loading || ''" :shape="cancelBtn.shape || ''" :size="cancelBtn.size || ''"
                        :type="cancelBtn.type || ''" @click="handleCancel" />
                </template>
                <slot name="cancel-btn" />
                <template v-if="confirmBtn">
                    <cy-button block :custom-class="`cy-dialog__button--${buttonLayout} ` + customClassConfirm"
                        :theme="confirmBtn.theme || 'primary'" :content="confirmBtn.content || '确定'"
                        :variant="confirmBtn.variant || ''" :ghost="confirmBtn.ghost || ''"
                        :icon="confirmBtn.icon || ''" :loading="confirmBtn.loading || ''"
                        :shape="confirmBtn.shape || ''" :size="confirmBtn.size || ''" :type="confirmBtn.type || ''"
                        @click="handleConfirm" />
                </template>
                <slot name="confirm-btn" />
            </view>
        </view>
    </cy-popup>
</template>

<script>
export default {
    name: 'dialog',
    externalClasses: [
        'custom-class',
        'custom-class-content',
        'custom-class-confirm',
        'custom-class-cancel',
        'custom-class-action'
    ],
    options: {
        styleIsolation: 'shared',
        addGlobalClass: true,
        virtualHost: true,
        externalClasses: true
    },
    props: {
        /** 多按钮排列方式 */
        buttonLayout: {
            type: String,
            default: 'horizontal'
        },
        /** 取消按钮，可自定义。值为 null 则不显示取消按钮。值类型为字符串，则表示自定义按钮文本，值类型为 Object 则表示透传 Button 组件属性。使用 TNode 自定义按钮时，需自行控制取消事件 */
        cancelBtn: {
            type: [Object, String],
            default: null
        },
        /** 是否展示关闭按钮，值为 `true` 显示默认关闭按钮；值为 `false` 则不显示关闭按钮；使用 Object 时透传至图标组件 */
        closeBtn: {
            type: Boolean,
            default: false
        },
        /** 点击蒙层时是否触发关闭事件 */
        closeOnOverlayClick: {
            type: Boolean,
            default: false
        },
        /** 确认按钮。值为 null 则不显示确认按钮。值类型为字符串，则表示自定义按钮文本，值类型为 Object 则表示透传 Button 组件属性。使用 TNode 自定义按钮时，需自行控制确认事件 */
        confirmBtn: {
            type: [Object, String],
            default: null
        },
        /** 内容 */
        content: {
            type: String
        },
        /** 标题 */
        title: {
            type: String
        },
        /** 对话框层级，Web 侧样式默认为 2500，移动端样式默认 2500，小程序样式默认为 11500 */
        zIndex: {
            type: Number,
            default: 11500
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
        customClassAction: {
            type: [String, Array],
            default: ''
        },
        customClassCancel: {
            type: [String, Array],
            default: ''
        },
        customClassConfirm: {
            type: [String, Array],
            default: ''
        },
    },
    data() {
        return {
            loading: false,
            popupRef: 'modalPopup'
        };
    },
    methods: {
        open() {
            this.$refs[this.popupRef].open();
            if (this.loading) this.loading = false;
        },
        close() {
            this.$refs[this.popupRef].close();
        },
        handleClose() {
            this.$refs[this.popupRef].close();
            this.$emit('close');
        },
        handleConfirm(event) {
            if (!this.loading) {
                this.$emit('confirm', event);
            }
        },
        handleCancel(event) {
            this.$refs[this.popupRef].close();
            this.$emit('cancel', event);
        }
    },
    // 组件周期函数--监听组件挂载完毕
    mounted() { },
    // 组件周期函数--监听组件数据更新之前
    beforeUpdate() { },
    // 组件周期函数--监听组件数据更新之后
    updated() { },
    // 组件周期函数--监听组件激活(显示)
    activated() { },
    // 组件周期函数--监听组件停用(隐藏)
    deactivated() { },
    // 组件周期函数--监听组件销毁之前
    beforeDestroy() { }
};
</script>

<style lang="scss">
@import './dialog.scss';
</style>
