<template>
	<view :class="['cy-checkbox-group', customClass]">
		<slot></slot>
	</view>
</template>

<script>
export default {
	name: 'checkbox-group',
	externalClasses: ['custom-class'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		value: {
			type: Array,
			default: null
		},
		disabled: {
			type: Boolean,
			default: false
		},
		max: {
			type: Number,
			default: null
		},
		borderless: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
	},
	watch: {
		value: {
			immediate: true,
			deep: true,
			handler(value) {
				this.currentValue = value || []
				this.deepSetValue(this.$children)
			}
		}
	},
	data() {
		return {
			currentValue: []
		}
	},
	methods: {
		/**
		 * @description evan-checkbox状态变更
		 * @function onCheckboxChange
		 * @param {boolean} [flag=true] 是否触发change事件，主动调用全选，反选，清空均不触发change事件
		 */
		onCheckboxChange(name, flag = true) {
			const value = this.currentValue || []
			const index = value.findIndex((v) => v === name)
			if (index !== -1) {
				value.splice(index, 1)
			} else {
				value.push(name)
			}
			this.currentValue = value
			this.$emit('input', value)
			if (flag) {
				this.$emit('change', value)
			}
		},
		deepSetValue(array) {
			if (Array.isArray(array)) {
				array.forEach((child) => {
					let childName = child.$options.name
					if (childName === 'checkbox') {
						if (typeof child.setValue === 'function') {
							child.setValue(this.value)
						}
					} else if (child.$children) {
						this.deepSetValue(child.$children)
					}
				})
			}
		},
		deepDirectSetValue(array, value) {
			if (Array.isArray(array)) {
				array.forEach((child) => {
					let childName = child.$options.name
					if (childName === 'checkbox') {
						if (typeof child.directSetValue === 'function') {
							child.directSetValue(value)
						}
					} else if (child.$children) {
						this.deepDirectSetValue(child.$children, value)
					}
				})
			}
		},
		deepReverseValue(array) {
			if (Array.isArray(array)) {
				array.forEach((child) => {
					let childName = child.$options.name
					if (childName === 'checkbox') {
						if (typeof child.reverseValue === 'function') {
							child.reverseValue()
						}
					} else if (child.$children) {
						this.deepReverseValue(child.$children)
					}
				})
			}
		},
		selectAll() {
			this.deepDirectSetValue(this.$children, true)
		},
		selectReverse() {
			this.deepReverseValue(this.$children)
		},
		clearAll() {
			this.deepDirectSetValue(this.$children, false)
		}
	}
}
</script>