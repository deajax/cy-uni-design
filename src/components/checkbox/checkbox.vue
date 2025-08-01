<template>
	<view :class="['cy-checkbox', setPlacement, setBlock, customClass]" @click="onCheckboxChange">
		<view :class="['cy-checkbox__icon',
			`cy-checkbox__icon--${placement}`,
			currentValue && 'cy-checkbox__icon--checked',
			isDisabled && 'cy-checkbox__icon--disabled', customClassIcon]">
			<slot v-if="$slots.icon" name="icon"></slot>
			<template v-else>
				<cy-icon v-if="icon" :name="icon" custom-class="cy-radio__icon-wrap" />
				<cy-icon v-else
						 :name="currentValue ? 'checkbox-circle-fill' : 'checkbox-blank-circle-line'"
						 custom-class="cy-radio__icon-wrap" />
			</template>
		</view>
		<view :class="['cy-checkbox__content', customClassContent]">
			<view :class="['cy-checkbox__title',
				currentValue && 'cy-checkbox__title--checked',
				isDisabled && 'cy-checkbox__title--disabled', customClassTitle]">
				<template v-if="label">{{ label }}</template>
				<slot />
				<slot name="label" v-if="$slots.label" />
			</view>
			<view v-if="$slots.content || content" :class="['cy-checkbox__description',
				currentValue && 'cy-checkbox__description--checked',
				isDisabled && 'cy-checkbox__description--disabled', customClassDescription]">
				{{ content }}
				<slot name="content" />
			</view>
		</view>
		<view v-if="!isBorderless" :class="['cy-checkbox__border', `cy-checkbox__border--${placement}`]" />
	</view>
</template>

<script>
export default {
	name: 'checkbox',
	externalClasses: ['custom-class', 'custom-class-icon', 'custom-class-conetnt', 'custom-class-title', 'custom-class-description'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		value: {
			type: Boolean,
			default: false
		},
		name: {
			type: [String, Number, Boolean],
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
		icon: {
			type: String,
			default: null
		},
		preventClick: {
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
		isOverLimit() {
			if (this.isGroup) {
				let parent = this.getParent()
				if (parent.max) {
					let parentValue = parent.currentValue || []
					if (parentValue.length >= parent.max) {
						return true
					}
				}
			}
			return false
		},

		setPlacement() {
			if (this.placement) {
				return 'cy-checkbox--' + this.placement
			}
		},
		setBlock() {
			if (this.isBorderless) return;
			if (this.block) {
				return 'cy-checkbox--block'
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
		// 获取EvanCheckboxGroup组件
		getParent() {
			let parent = this.$parent
			if (parent) {
				let parentName = parent.$options.name
				while (parentName !== 'checkbox-group') {
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
		// 点击触发
		onCheckboxChange() {
			if (!this.isDisabled && !this.preventClick && (!this.isOverLimit || this.currentValue)) {
				this.toggleValue()
			}
		},
		// 主动调用方法触发
		toggle() {
			if (!this.isDisabled && (!this.isOverLimit || this.currentValue)) {
				this.toggleValue()
			}
		},
		// 切换状态
		toggleValue() {
			this.currentValue = !this.currentValue
			this.$emit('input', this.currentValue)
			this.$emit('change', this.currentValue)
			let parent = this.getParent()
			if (parent) {
				parent.onCheckboxChange(this.name)
			}
		},
		// 根据EvanCheckboxGroup组件的值设置当前checkbox的值
		setValue(groupValue) {
			groupValue = groupValue || []
			this.currentValue = groupValue.includes(this.name)
		},
		// EvanCheckboxGroup组件直接设置当前checkbox的值
		directSetValue(value) {
			let parent = this.getParent()
			if (parent) {
				if (value !== this.currentValue) {
					parent.onCheckboxChange(this.name, false)
				}
			}
		},
		// EvanCheckboxGroup组件直接反向设置当前checkbox的值
		reverseValue() {
			let parent = this.getParent()
			if (parent) {
				parent.onCheckboxChange(this.name, false)
			}
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
@import './checkbox.scss';
</style>
