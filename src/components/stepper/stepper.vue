<template>
	<view :class="['cy-stepper', `cy-stepper--${size}`, customClass]">
		<view
			:class="[
				'cy-stepper__minus',
				`cy-stepper__minus--${theme}`,
				`cy-stepper__icon--${size}`,
				customClassMinus,
				inputValue <= min || disabled ? `cy-stepper--${theme}-disabled` : '',
			]"
			hover-class="cy-stepper--hover"
			@click="_calcValue('minus')"
		>
			<cy-icon name="subtract-line" custom-class="cy-stepper__minus-icon" />
			<slot name="minus" />
		</view>

		<view :class="[`cy-stepper__input--${theme}`, customClassInput]">
			<input
				v-model="inputValue"
				:style="inputWidth ? 'width: ' + widthWithPx : ''"
				:class="[
					'cy-stepper__input',
					`cy-stepper__input--${size}`,
					disabled ? `cy-stepper--${theme}-disabled` : '',
				]"
				:disabled="disabled || disableInput"
				:type="step > 0 && step < 1 ? 'digit' : 'number'"
				:placeholder="''"
				:enableNative="false"
				@focus="_onFocus"
				@blur="_onBlur"
			/>
			<slot name="input" />
		</view>

		<view
			:class="[
				'cy-stepper__plus',
				`cy-stepper__plus--${theme}`,
				`cy-stepper__icon--${size}`,
				customClassPlus,
				inputValue >= max || disabled ? `cy-stepper--${theme}-disabled` : '',
			]"
			hover-class="cy-stepper--hover"
			@click="_calcValue('plus')"
		>
			<cy-icon name="add-line" custom-class="cy-stepper__plus-icon" />
			<slot name="plus" />
		</view>

		<slot />
	</view>
</template>

<script>
	import cyIcon from "../icon/icon.vue";

	export default {
		name: "stepper",
		components: {
			cyIcon,
		},
		externalClasses: [
			"custom-class",
			"custom-class-input",
			"custom-class-minus",
			"custom-class-plus",
		],
		options: {
			styleIsolation: "shared",
			addGlobalClass: true,
			virtualHost: true,
			externalClasses: true,
		},
		emits: ["change", "input", "update:modelValue", "blur", "focus", "overlimit"],
		props: {
			value: {
				type: [Number, String],
				default: 1,
			},
			modelValue: {
				type: [Number, String],
				default: 1,
			},
			/** 最小值 */
			min: {
				type: Number,
				default: 0,
			},
			/** 最大值 */
			max: {
				type: Number,
				default: 100,
			},
			/** 步长 */
			step: {
				type: Number,
				default: 1,
			},
			background: {
				type: String,
				default: "#f5f5f5",
			},
			color: {
				type: String,
				default: "#333",
			},
			/** 输入框宽度 */
			inputWidth: {
				type: Number,
				default: 40,
			},
			/** 禁用全部操作 */
			disabled: {
				type: Boolean,
				default: false,
			},
			/** 禁用输入框 */
			disableInput: {
				type: Boolean,
				default: false,
			},
			/** 组件尺寸 */
			size: {
				type: String,
				default: "medium",
			},
			/** 组件风格 */
			theme: {
				type: String,
				default: "normal",
			},

			// externalClasses
			customClass: {
				type: [String, Array],
				default: "",
			},
			customClassMinus: {
				type: [String, Array],
				default: "",
			},
			customClassInput: {
				type: [String, Array],
				default: "",
			},
			customClassPlus: {
				type: [String, Array],
				default: "",
			},
		},
		data() {
			return {
				inputValue:
					this.modelValue !== 1 ? Number(this.modelValue) : Number(this.value),
			};
		},
		watch: {
			value(val) {
				this.inputValue = +val;
			},
			modelValue(val) {
				this.inputValue = +val;
			},
		},
		computed: {
			widthWithPx() {
				// 确保返回有效的像素值
				return (this.inputWidth || 40) + "px";
			},
		},
		created() {
			// 简化初始化逻辑
			const value = this.modelValue !== 1 ? this.modelValue : this.value;
			this.inputValue = Number(value);

			// 确保值在有效范围内
			this.inputValue = Math.min(Math.max(this.inputValue, this.min), this.max);
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
					if (value < this.min * scale) {
						this.$emit("overlimit", type);
						return;
					}
					if (value > this.max * scale) {
						value = this.max * scale;
					}
				}

				if (type === "plus") {
					value += step;
					if (value > this.max * scale) {
						this.$emit("overlimit", type);
						return;
					}
					if (value < this.min * scale) {
						value = this.min * scale;
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
				this.$emit("blur", event);
				let value = event.detail.value;

				// 处理空值情况
				if (value === "" || value === null || value === undefined) {
					this.inputValue = this.min;
					this.$emit("input", this.min);
					this.$emit("update:modelValue", this.min);
					this.$emit("change", this.min);
					return;
				}

				if (isNaN(value)) {
					this.inputValue = this.min;
				} else {
					value = +value;
					if (value > this.max) {
						value = this.max;
					} else if (value < this.min) {
						value = this.min;
					}
					this.inputValue = value;
				}

				// 保证精度
				const scale = this._getDecimalScale();
				this.inputValue = parseFloat(this.inputValue).toFixed(
					String(scale).length - 1
				);
				this.$emit("input", +this.inputValue);
				this.$emit("update:modelValue", +this.inputValue);
				this.$emit("change", +this.inputValue);
			},
			_onFocus(event) {
				this.$emit("focus", event);
			},
		},
		mounted() {
			// 检查 cy-icon 是否正确加载
			if (!this.$options.components.cyIcon) {
				console.warn("cy-stepper: cy-icon component is not registered");
			}
		},
	};
</script>

<style lang="scss">
	@import "./stepper.scss";
</style>
