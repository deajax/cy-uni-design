<template>
	<view :class="['cy-stepper', `cy-stepper--${size}`, customClass]">
		<view :class="['cy-stepper__minus', `cy-stepper__minus--${theme}`, `cy-stepper__icon--${size}`, customClassMinus, inputValue <= min || disabled ? `cy-stepper--${theme}-disabled` : '']"
			  hover-class="cy-stepper--hover"
			  @click="_calcValue('minus')">
			<cy-icon name="subtract-line" custom-class="cy-stepper__minus-icon" />
			<slot name="minus" />
		</view>

		<view :class="[`cy-stepper__input--${theme}`, customClassInput]">
			<input
				   v-model="inputValue"
				   :style="inputWidth ? { width: widthWithPx } : ''"
				   :class="['cy-stepper__input', `cy-stepper__input--${size}`, disabled || disableInput ? `cy-stepper--${theme}-disabled` : '']"
				   :disabled="disabled || disableInput"
				   :type="step < 1 ? 'digit' : 'number'"
				   :placeholder="null"
				   :enableNative="false"
				   @focus="_onFocus"
				   @blur="_onBlur" />
			<slot name="input" />
		</view>
		<slot />

		<view :class="['cy-stepper__plus', `cy-stepper__plus--${theme}`, `cy-stepper__icon--${size}`, customClassPlus, inputValue >= max || disabled ? `cy-stepper--${theme}-disabled` : '']"
			  hover-class="cy-stepper--hover"
			  @click="_calcValue('plus')">
			<cy-icon name="add-line" custom-class="cy-stepper__plus-icon" />
			<slot name="plus" />
		</view>
	</view>
</template>

<script>
export default {
	name: "stepper",
	externalClasses: ['custom-class', 'custom-class-input', 'custom-class-minus', 'custom-class-plus'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	emits: ['change', 'input', 'update:modelValue', 'blur', 'focus'],
	props: {
		value: {
			type: [Number, String],
			default: 1
		},
		modelValue: {
			type: [Number, String],
			default: 1
		},
		/** 最小值 */
		min: {
			type: Number,
			default: 0
		},
		/** 最大值 */
		max: {
			type: Number,
			default: 100
		},
		/** 步长 */
		step: {
			type: Number,
			default: 1
		},
		background: {
			type: String,
			default: '#f5f5f5'
		},
		color: {
			type: String,
			default: '#333'
		},
		/** 输入框宽度 */
		inputWidth: {
			type: Number,
			default: 40,
		},
		/** 禁用全部操作 */
		disabled: {
			type: Boolean,
			default: false
		},
		/** 禁用输入框 */
		disableInput: {
			type: Boolean,
			default: false
		},
		/** 组件尺寸 */
		size: {
			type: String,
			default: 'medium',
		},
		/** 组件风格 */
		theme: {
			type: String,
			default: 'normal',
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassMinus: {
			type: [String, Array],
			default: ''
		},
		customClassInput: {
			type: [String, Array],
			default: ''
		},
		customClassPlus: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			inputValue: 0
		};
	},
	watch: {
		value(val) {
			this.inputValue = +val;
		},
		modelValue(val) {
			this.inputValue = +val;
		}
	},
	computed: {
		widthWithPx() {
			return this.inputWidth + 'px';
		}
	},
	created() {
		if (this.value === 1) {
			this.inputValue = +this.modelValue;
		}
		if (this.modelValue === 1) {
			this.inputValue = +this.value;
		}
	},
	methods: {
		_calcValue(type) {
			if (this.disabled) {
				return;
			}
			const scale = this._getDecimalScale();
			let value = this.inputValue * scale;
			let step = this.step * scale;
			if (type === "minus") {
				value -= step;
				if (value < (this.min * scale)) {
					return;
				}
				if (value > (this.max * scale)) {
					value = this.max * scale
				}
			}

			if (type === "plus") {
				value += step;
				if (value > (this.max * scale)) {
					return;
				}
				if (value < (this.min * scale)) {
					value = this.min * scale
				}
			}

			this.inputValue = (value / scale).toFixed(String(scale).length - 1);
			// TODO vue2 兼容
			this.$emit("input", +this.inputValue);
			// TODO vue3 兼容
			this.$emit("update:modelValue", +this.inputValue);
			this.$emit("change", +this.inputValue);
		},
		_getDecimalScale() {

			let scale = 1;
			// 浮点型
			if (~~this.step !== this.step) {
				scale = Math.pow(10, String(this.step).split(".")[1].length);
			}
			return scale;
		},
		_onBlur(event) {
			this.$emit('blur', event)
			let value = event.detail.value;
			if (isNaN(value)) {
				this.inputValue = this.value;
				return;
			}
			value = +value;
			if (value > this.max) {
				value = this.max;
			} else if (value < this.min) {
				value = this.min;
			}
			const scale = this._getDecimalScale();
			this.inputValue = value.toFixed(String(scale).length - 1);
			this.$emit("input", +this.inputValue);
			this.$emit("update:modelValue", +this.inputValue);
			this.$emit("change", +this.inputValue);
		},
		_onFocus(event) {
			this.$emit('focus', event)
		}
	}
} 
</script>

<style lang="scss">
@import './stepper.scss';
</style>