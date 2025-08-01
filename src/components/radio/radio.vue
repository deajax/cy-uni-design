<template>
	<view :class="['cy-radio', setPlacement, setBlock, customClass]" @click="onRadioClick">
		<view :class="['cy-radio__icon',
		isChecked && 'cy-radio__icon--checked',
		isDisabled && 'cy-radio__icon--disabled', customClassIcon]">
			<slot v-if="$slots.icon" name="icon"></slot>
			<template v-else>
				<cy-icon v-if="icon"
						 :name="icon"
						 :size="48"
						 custom-class="cy-radio__icon-wrap" />
				<cy-icon v-else
						 :name="isChecked ? 'radio-button-line' : 'checkbox-blank-circle-line'"
						 :size="48"
						 custom-class="cy-radio__icon-wrap" />
			</template>
		</view>
		<view :class="['cy-radio__content', customClassContent]">
			<view :class="['cy-radio__title',
		isChecked && 'cy-radio__title--checked',
		isDisabled && 'cy-radio__title--disabled', customClassTitle]">
				<template v-if="label">{{ label }}</template>
				<slot />
				<slot name="label" v-if="$slots.label" />
			</view>
			<view v-if="$slots.content || content"
				  :class="['cy-radio__description',
		isChecked && 'cy-radio__description--checked',
		isDisabled && 'cy-radio__description--disabled', customClassDescription]">
				{{ content }}
				<slot name="content" />
			</view>
		</view>
		<view v-if="!isBorderless" :class="['cy-radio__border', `cy-radio__border--${placement}`]" />
	</view>
</template>

<script>
export default {
	name: 'radio',
	externalClasses: ['custom-class', 'custom-class-icon', 'custom-class-conetnt', 'custom-class-title', 'custom-class-description'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		value: {
			type: [String, Number, Boolean],
			default: null
		},
		name: {
			type: [String, Number, Boolean],
			default: null
		},
		icon: {
			type: String,
			default: null
		},
		label: {
			type: String,
			default: null
		},
		content: {
			type: String,
			default: null
		},
		disabled: {
			type: Boolean,
			default: false
		},
		preventClick: {
			type: Boolean,
			default: false
		},
		clearable: {
			type: Boolean,
			default: false
		},
		placement: {
			type: String,
			default: 'left'
		},
		block: {
			type: Boolean,
			default: true
		},
		borderless: {
			type: Boolean,
			default: false
		},

		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassIcon: {
			type: [String, Array],
			default: ''
		},
		customClassContent: {
			type: [String, Array],
			default: ''
		},
		customClassTitle: {
			type: [String, Array],
			default: ''
		},
		customClassDescription: {
			type: [String, Array],
			default: ''
		},
	},
	computed: {
		isGroup() {
			let parent = this.getParent()
			if (parent) {
				return true
			}
			return false
		},
		isBorderless() {
			if (this.isGroup) {
				return this.getParent().borderless || this.borderless
			}
			return this.borderless
		},
		isDisabled() {
			if (this.isGroup) {
				return this.getParent().disabled || this.disabled
			}
			return this.disabled
		},
		isChecked() {
			let parent = this.getParent()
			if ((this.isGroup && parent.value === this.name) || (!this.isGroup && this.currentValue === this.name)) {
				return true
			}
			return false
		},

		setPlacement() {
			if (this.placement) {
				return 'cy-radio--' + this.placement
			}
		},
		setBlock() {
			if (this.isBorderless) return;
			if (this.block) {
				return 'cy-radio--block'
			}
		},
	},
	watch: {
		value: {
			immediate: true,
			handler(value) {
				this.currentValue = value
			}
		}
	},
	data() {
		return {
			currentValue: null
		}
	},
	methods: {
		// 获取EvanRadioGroup组件
		getParent() {
			let parent = this.$parent
			if (parent) {
				let parentName = parent.$options.name
				while (parentName !== 'radio-group') {
					parent = parent.$parent
					if (parent) {
						parentName = parent.$options.name
					} else {
						return null
					}
				}
				return parent
			}
			return null
		},
		onRadioClick() {
			if (!this.isDisabled && !this.preventClick) {
				this.choose()
			}
		},
		select() {
			if (!this.isDisabled) {
				this.choose()
			}
		},
		choose() {
			if (this.currentValue !== this.name) {
				this.currentValue = this.name
				this.$emit('input', this.currentValue)
				this.$emit('change', this.currentValue)
				if (this.isGroup) {
					let parent = this.getParent()
					parent.onRadioChange(this.name)
				}
			} else if (this.clearable) {
				this.currentValue = null
				this.$emit('input', this.currentValue)
				this.$emit('change', this.currentValue)
				if (this.isGroup) {
					let parent = this.getParent()
					parent.onRadioChange(null)
				}
			}
		},
		setValue(groupValue) {
			this.currentValue = groupValue
		}
	},
	created() {
		let parent = this.getParent()
		if (parent) {
			this.setValue(parent.value)
		}
	}
}
</script>

<style lang="scss">
@import './radio.scss';
</style>
