<template>
	<view :class="['cy-radio-group', customClass]">
		<slot></slot>
	</view>
</template>

<script>
export default {
	name: 'radio-group',
	externalClasses: ['custom-class'],
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
		disabled: {
			type: Boolean,
			default: false
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
			handler(value) {
				this.deepSetValue(this.$children)
			}
		}
	},
	methods: {
		onRadioChange(name) {
			this.$emit('input', name)
			this.$emit('change', name)
		},
		deepSetValue(array) {
			if (Array.isArray(array)) {
				array.forEach((child) => {
					let childName = child.$options.name
					if (childName === 'radio') {
						if (typeof child.setValue === 'function') {
							child.setValue(this.value)
						}
					} else if (child.$children) {
						this.deepSetValue(child.$children)
					}
				})
			}
		}
	}
}
</script>