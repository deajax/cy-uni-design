<template>
	<view
		  :style="[textareaStyle]"
		  :class="['cy-textarea', bordered ? 'cy-textarea--border' : '', customClass]">
		<view :class="['cy-textarea__label', customClassLabel]">
			<template v-if="label">{{ label }}</template>
			<slot name="label" />
		</view>
		<view :class="['cy-textarea__wrapper', customClassWrapper]">
			<textarea
					  :class="['cy-textarea__wrapper-inner', disabled ? 'is-disabled' : '']"
					  :style="[customStyle]"
					  :maxlength="maxlength"
					  :disabled="disabled"
					  :placeholder="placeholder"
					  :placeholder-class="['cy-textarea__placeholder']"
					  :placeholder-style="placeholderStyle"
					  :value="innerValue"
					  :auto-height="autosize"
					  :auto-focus="autofocus"
					  :fixed="fixed"
					  :focus="focus"
					  :cursor="cursor"
					  :cursor-spacing="cursorSpacing"
					  :adjust-position="adjustPosition"
					  :confirm-type="confirmType"
					  :confirm-hold="confirmHold"
					  :disable-default-padding="disableDefaultPadding"
					  :show-confirm-bar="showConfirmBar"
					  :show-count="false"
					  :selection-start="selectionStart"
					  :selection-end="selectionEnd"
					  :hold-keyboard="holdKeyboard"
					  @input="onInput"
					  @focus="onFocus"
					  @blur="onBlur"
					  @confirm="onConfirm"
					  @linechange="onLineChange"
					  @keyboardheightchange="onKeyboardHeightChange" />
			<view v-if="indicator && (maxcharacter > 0 || maxlength > 0)"
				  :class="['cy-textarea__indicator', customClassIndicator]">
				{{ innerValue !== null && innerValue !== undefined ? innerValue.length : '0' }}
				/
				{{ maxcharacter || maxlength }}
			</view>
		</view>
		<slot />
	</view>
</template>

<script>
export default {
	name: "textarea",
	externalClasses: ['custom-class', 'custom-class-label', 'custom-class-wrapper', 'custom-class-indicator'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		/** 键盘弹起时，是否自动上推页面 */
		adjustPosition: {
			type: Boolean,
			default: true,
		},
		/** 自动聚焦，拉起键盘 */
		autofocus: {
			type: Boolean,
			default: false,
		},
		/** 是否自动增高，值为 autosize 时，style.height 不生效 */
		autosize: {
			type: null,
			default: false,
		},
		/** 点击键盘右下角按钮时是否保持键盘不收起点 */
		confirmHold: {
			type: Boolean,
			default: false,
		},
		/** 设置键盘右下角按钮的文字，仅在 type='text'时生效 */
		confirmType: {
			type: String,
			default: 'return',
		},
		/** 指定光标与键盘的距离。取textarea距离底部的距离和cursor-spacing指定的距离的最小值作为光标与键盘的距离 */
		cursorSpacing: {
			type: Number,
			default: 0,
		},
		/** 是否禁用文本框 */
		disabled: {
			type: Boolean,
			default: false,
		},
		/** 自动聚焦 */
		focus: {
			type: Boolean,
			default: false,
		},
		/** 左侧文本 */
		label: {
			type: String,
		},
		/** 如果 textarea 是在一个 `position:fixed` 的区域，需要显示指定属性 fixed 为 true */
		fixed: {
			type: Boolean,
			default: false,
		},
		/** 用户最多可以输入的字符个数，一个中文汉字表示两个字符长度 */
		maxcharacter: {
			type: Number,
		},
		/** 用户最多可以输入的字符个数。默认为 -1，不限制输入长度 */
		maxlength: {
			type: Number,
			default: -1,
		},
		/** 指定 placeholder 的样式，目前仅支持 color ,font-size和font-weight */
		placeholder: {
			type: String,
			default: undefined,
		},
		/** 占位符样式 */
		placeholderStyle: {
			type: String,
			default: '',
		},
		/** 文本框值 */
		value: {
			type: String,
			default: null,
		},
		/** 文本框值，非受控属性 */
		defaultValue: {
			type: String,
			default: '',
		},
		/** 是否显示外边框 */
		bordered: {
			type: Boolean,
			default: false,
		},
		/**
		 * 显示文本计数器，如 0/140。当 `maxlength < 0 && maxcharacter < 0` 成立时， indicator无效
		 */
		indicator: {
			type: Boolean,
			default: false,
		},
		/** 指定focus时的光标位置 */
		cursor: {
			type: Number,
			default: -1,
		},
		/** 是否显示键盘上方带有”完成“按钮那一栏 */
		showConfirmBar: {
			type: Boolean,
			default: true,
		},
		/** 光标起始位置，自动聚集时有效，需与selection-end搭配使用 */
		selectionStart: {
			type: Number,
			default: -1,
		},
		/** 光标结束位置，自动聚集时有效，需与selection-start搭配使用 */
		selectionEnd: {
			type: Number,
			default: -1,
		},
		/** 是否去掉 iOS 下的默认内边距 */
		disableDefaultPadding: {
			type: Boolean,
			default: false,
		},
		/** focus时，点击页面的时候不收起键盘 */
		holdKeyboard: {
			type: Boolean,
			default: false,
		},
		customStyle: {
			type: [String, Object],
			default: { height: '96px' },
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassLabel: {
			type: [String, Array],
			default: ''
		},
		customClassWrapper: {
			type: [String, Array],
			default: ''
		},
		customClassIndicator: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			// 输入框的值
			innerValue: "",
			// 是否处于获得焦点状态
			focused: false,
			// value是否第一次变化，在watch中，由于加入immediate属性，会在第一次触发，此时不应该认为value发生了变化
			firstChange: true,
			// value绑定值的变化是由内部还是外部引起的
			changeFromInner: false,
			// 过滤处理方法
			innerFormatter: value => value
		}
	},
	watch: {
		value: {
			immediate: true,
			handler(newVal, oldVal) {
				this.innerValue = newVal;
				/* #ifdef H5 */
				// 在H5中，外部value变化后，修改input中的值，不会触发@input事件，此时手动调用值变化方法
				if (
					this.firstChange === false &&
					this.changeFromInner === false
				) {
					this.valueChange();
				}
				/* #endif */
				this.firstChange = false;
				// 重置changeFromInner的值为false，标识下一次引起默认为外部引起的
				this.changeFromInner = false;
			},
		},
	},
	computed: {
		textareaStyle() {
			const style = {};
			uni.getSystemInfo({
				success: (res) => {
					if (res.osName === 'android') {
						style.padding = "6px 6px 3px 9px";
					}
				},
			})
		},
	},
	methods: {
		setFormatter(e) {
			this.innerFormatter = e
		},
		onInput(e) {
			let { value = "" } = e.detail || {};
			// 格式化过滤方法
			const formatter = this.formatter || this.innerFormatter
			const formatValue = formatter(value)
			// 为了避免props的单向数据流特性，需要先将innerValue值设置为当前值，再在$nextTick中重新赋予设置后的值才有效
			this.innerValue = value
			this.$nextTick(() => {
				this.innerValue = formatValue;
				this.valueChange();
			})
		},
		// 内容发生变化，进行处理
		valueChange() {
			const value = this.innerValue;
			this.$nextTick(() => {
				this.$emit("input", value);
				// 标识value值的变化是由内部引起的
				this.changeFromInner = true;
				this.$emit("change", value);
			});
		},
		onFocus(e) {
			this.$emit("focus", e);
		},
		onBlur(e) {
			this.$emit("blur", e);
		},
		onConfirm(e) {
			this.$emit("confirm", e);
		},
		onLineChange(e) {
			this.$emit("linechange", e);
		},
		onKeyboardHeightChange(e) {
			this.$emit("keyboardheightchange", e);
		},
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
	beforeDestroy() { },
} 
</script>

<style lang="scss">
@import './textarea.scss';
</style>