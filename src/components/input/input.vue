<template>
	<view :class="['cy-input', `cy-input--layout-${layout}`, customClass, setClass]" :style="style" @tap="handleTap">
		<view :class="['cy-input__wrap--prefix', customClassPrefix]">
			<view :class="['cy-input__icon--prefix', customClassPrefixIcon]" v-if="prefixIcon || $slots['prefix-icon']"
				  @click="onPrefixClick">
				<slot name="prefix-icon" />
				<cy-icon v-if="prefixIcon"
						 :name="prefixIcon.name || prefixIcon"
						 :size="prefixIcon.size || ''"
						 :color="prefixIcon.color || ''"
						 custom-class="cy-input__prefix-icon" />
			</view>
			<view :class="['cy-input__label', customClassLabel]" v-if="label">
				<slot name="label" />
				{{ label }}
                <cy-icon v-if="required"
                         name="asterisk"
                         size="20"
                         color="var(--cell-required-color, #ef4444)"
                         :custom-style="{ marginLeft: '8rpx' }" />
			</view>
		</view>
		<view class="cy-input__wrap">
			<view :class="['cy-input__content', `cy-input--${status}`, customClassContent]">
				<slot name="input" v-if="$slots.input" />
				<input v-else
					   :class="['cy-input__control', `cy-input--${align}`, disabled && 'cy-input__control--disabled', customClassInput]"
					   :value="keyword"
					   :placeholder="placeholder"
					   :placeholder-style="placeholderStyle"
					   :placeholder-class="['cy-input__placeholder', placeholderClass]"
					   :maxlength="maxlength"
					   :disabled="disabled"
					   @input="onInput"
					   @focus="onFocus"
					   @blur="onBlur"
					   @confirm="onConfirm"
					   @keyboardheightchange="onKeyboardHeightChange"
					   @nicknamereview="onNickNameReview"
					   :enableNative="false"
					   :password="type === 'password'"
					   :type="type === 'password' ? 'text' : type"
					   :focus="focus"
					   :confirm-type="confirmType"
					   :confirm-hold="confirmHold"
					   :cursor="cursor"
					   :cursor-spacing="cursorSpacing"
					   :adjust-position="adjustPosition"
					   :auto-focus="autoFocus"
					   :always-embed="alwaysEmbed"
					   :selection-start="selectionStart"
					   :selection-end="selectionEnd"
					   :hold-keyboard="holdKeyboard">
				<view class="cy-input__wrap--clearable-icon"
					  v-if="keyword !== '' && clearable && focused"
					  @click="onClear">
					<cy-icon name="close-circle-fill" />
				</view>
				<view :class="['cy-input__wrap--suffix', customClassSuffix]" v-if="suffix || $slots.suffix">
					<text v-if="suffix">{{ suffix }}</text>
					<slot name="suffix" />
				</view>
				<view :class="['cy-input__wrap--suffix-icon'], customClassSuffixIcon"
					  v-if="suffixIcon || $slots['suffix-icon']" @click="onSuffixClick">
					<slot name="suffix-icon" />
					<cy-icon :name="suffixIcon.name || suffixIcon"
							 :size="suffixIcon.size || ''"
							 :color="suffixIcon.color || ''"
							 custom-class="cy-input__suffix-icon" />
				</view>
			</view>
			<view :class="['cy-input__tips', customClassTips]" v-if="tips && tips.length > 0">
				{{ tips }}
			</view>
			<slot name="tips" />
		</view>
	</view>
</template>

<script>
export default {
	name: "input",
	externalClasses: ['custom-class', 'custom-class-prefix', 'custom-class-prefix-icon', 'custom-class-label', 'custom-class-content', 'custom-class-input', 'custom-class-suffix', 'custom-class-suffix-icon', 'custom-class-tips'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		/** 文本内容位置，居左/居中/居右 */
		align: {
			type: String,
			default: 'left',
		},
		/** 标题输入框布局方式。可选项：vertical/horizontal */
		layout: {
			type: String,
			default: 'horizontal',
		},
		/** 是否开启无边框模式 */
		borderless: {
			type: Boolean,
			default: false,
		},
        /** 是否为必填项 */
        required: Boolean,
		/** 是否可清空 */
		clearable: {
			type: null,
			default: true,
		},
		/** 是否禁用输入框 */
		disabled: {
			type: Boolean,
			default: false,
		},
		/** 左侧文本 */
		label: {
			type: String,
		},
		/** 用户最多可以输入的字符个数，一个中文汉字表示两个字符长度。`maxcharacter` 和 `maxlength` 二选一使用 */
		maxcharacter: {
			type: Number,
		},
		/** 用户最多可以输入的文本长度，一个中文等于一个计数长度，默认为 -1，不限制输入长度。`maxcharacter` 和 `maxlength` 二选一使用 */
		maxlength: {
			type: Number,
			default: -1,
		},
		/** 占位符 */
		placeholder: {
			type: String,
			default: undefined,
		},
		/** 组件前置图标，值为字符串则表示图标名称 */
		prefixIcon: {
			type: null,
			default: null,
		},
		/** 输入框尺寸 */
		size: {
			type: String,
			default: 'medium',
		},
		/** 输入框状态 */
		status: {
			type: String,
			default: 'default',
		},
		/** 后置图标前的后置内容 */
		suffix: {
			type: String,
		},
		/** 后置文本内容，值为字符串则表示图标名称 */
		suffixIcon: {
			type: null,
			default: null,
		},
		/** 输入框下方提示文本，会根据不同的 `status` 呈现不同的样式 */
		tips: {
			type: String,
		},
		/** 输入框的值 */
		value: {
			type: String,
		},
		/** input 的类型。<br />具体释义：<br />`text` 文本输入键盘；<br />`number` 数字输入键盘；<br />`idcard` 身份证输入键盘；<br />`digit` 带小数点的数字键盘；<br />`safe-password` 密码安全输入键盘 <a href="https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/safe-password.html">指引</a>；<br />`nickname` 昵称输入键盘。<br />[小程序官方文档](https://developers.weixin.qq.com/miniprogram/dev/component/input.html) */
		type: {
			type: String,
			default: 'text',
		},
		/** 指定 placeholder 的样式 */
		placeholderStyle: {
			type: String,
			default: '',
		},
		/** 指定 placeholder 的样式类 */
		placeholderClass: {
			type: String,
			default: 'input-placeholder',
		},
		/** 指定光标与键盘的距离，取 input 距离底部的距离和 cursor-spacing 指定的距离的最小值作为光标与键盘的距离 */
		cursorSpacing: {
			type: Number,
			default: 0,
		},
		/** 获取焦点 */
		focus: {
			type: Boolean,
			default: false,
		},
		/** 设置键盘右下角按钮的文字，仅在type='text'时生效。<br />具体释义：<br />`send` 右下角按钮为“发送”；<br />`search` 右下角按钮为“搜索”；<br />`next` 右下角按钮为“下一个”；<br />`go` 右下角按钮为“前往”；<br />`done` 右下角按钮为“完成”。<br />[小程序官方文档](https://developers.weixin.qq.com/miniprogram/dev/component/input.html) */
		confirmType: {
			type: String,
			default: 'done',
		},
		/** 强制 input 处于同层状态，默认 focus 时 input 会切到非同层状态 (仅在 iOS 下生效) */
		alwaysEmbed: {
			type: Boolean,
			default: false,
		},
		/** 点击键盘右下角按钮时是否保持键盘不收起 */
		confirmHold: {
			type: Boolean,
			default: false,
		},
		/** 指定focus时的光标位置 */
		cursor: {
			type: Number,
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
		/** 键盘弹起时，是否自动上推页面 */
		adjustPosition: {
			type: Boolean,
			default: true,
		},
		/** focus时，点击页面的时候不收起键盘 */
		holdKeyboard: {
			type: Boolean,
			default: false,
		},
		style: {
			type: [Object, Array, String]
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassPrefix: {
			type: [String, Array],
			default: ''
		},
		customClassPrefixIcon: {
			type: [String, Array],
			default: ''
		},
		customClassLabel: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
		customClassInput: {
			type: [String, Array],
			default: ''
		},
		customClassSuffix: {
			type: [String, Array],
			default: ''
		},
		customClassSuffixIcon: {
			type: [String, Array],
			default: ''
		},
		customClassTips: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			keyword: '',
			focused: this.focus,
			innerFormatter: value => value
		}
	},
	computed: {
		setClass() {
			if (!this.borderless) {
				return 'cy-input--border'
			}
		},
		// #ifdef MP-ALIPAY
		placeholderStyle() {
			return 'text-indent: -4px;'
		}
		// #endif
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
			// 为了避免props的单向数据流特性，需要先将keyword值设置为当前值，再在$nextTick中重新赋予设置后的值才有效
			this.keyword = value
			this.$nextTick(() => {
				this.keyword = formatValue;
				this.valueChange();
			})
		},
		onFocus() {
			this.focused = true;
			this.$emit('focus', this.keyword);
		},
		onBlur() {
			setTimeout(() => {
				this.focused = false;
			}, 100)
			this.$emit('blur', this.keyword);
		},
		onConfirm(e) {
			this.$emit('enter', e.detail.value);
			try {
				uni.hideKeyboard();
			} catch (e) { }
		},
		onKeyboardHeightChange() {
			this.$emit("keyboardheightchange");
		},
		onNickNameReview() {
			this.$emit("nicknamereview");
		},
		// 内容发生变化，进行处理
		valueChange() {
			const value = this.keyword;
			this.$nextTick(() => {
				this.$emit("input", value);
				// 标识value值的变化是由内部引起的
				this.changeFromInner = true;
				this.$emit("change", value);
			});
		},
		onClear() {
			this.keyword = '';
			// 延后发出事件，避免在父组件监听clear事件时，value为更新前的值(不为空)
			this.$nextTick(() => {
				this.valueChange();
				this.$emit('clear');
			})
		},
		onPrefixClick(e) {
			this.$emit("prefix-click", e);
		},
		onSuffixClick(e) {
			this.$emit("suffix-click", e);
		},
        handleTap(event) {
            if (this.disabled) return;
            this.$emit('click', event);
            this.stop && this.preventEvent(event);
        }
	},
	watch: {
		keyword(e) {
			// 双向绑定值，让v-model绑定的值双向变化
			this.$emit('input', e);
			// 触发change事件，事件效果和v-model双向绑定的效果一样，让用户多一个选择
			this.$emit('change', e);
		},
		value: {
			immediate: true,
			handler(e) {
				this.keyword = e;
			}
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
	beforeDestroy() { },
} 
</script>

<style lang="scss">
@import './input.scss';
</style>