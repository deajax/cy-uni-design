<template>
	<view :class="['cy-search', customClass]">
        <slot name="prefix" />
		<view :class="['cy-search__content', `cy-search--${shape}`, customClassContent]" @click="clickHandler">
			<slot v-if="$slots['left-icon']" name="left-icon" />
			<cy-icon v-else :name="leftIcon" size="40"
					 :custom-class="'cy-search__content--icon ' + customClassLeftIcon" />
			<slot name="input" v-if="$slots.input" />
			<input
				   v-else
				   :class="['cy-search__content--input', customClassInput]"
				   :value="value"
				   :confirm-type="confirmType"
				   :type="type"
				   :placeholder="placeholder"
				   :placeholder-style="placeholderStyle"
				   :placeholder-class="placeholderClass"
				   :disabled="disabled"
				   :focus="focus"
				   :auto-blur="autoBlur"
				   :hold-keyboard="holdKeyboard"
				   @input="onInput"
				   @focus="onFocus"
				   @blur="onBlur"
				   @confirm="onConfirm" />
			<view v-if="keyword !== '' && clearable && focused"
				  :class="['cy-search__content--clearable', customClassClearable]"
				  aria-role="button" aria-label="清除"
                  hover-class="cy-search__content--clearable-hover"
				  @click="handleClear">
				<cy-icon name="close-circle-fill" size="32" color="#393939" />
			</view>
		</view>
		<view :class="['cy-search__action', customClassAction]" v-if="action || $slots.action" @click="onActionClick">
			{{ action }}
			<slot name="action" />
		</view>
		<cy-icon v-if="rightIcon" :name="rightIcon" size="40"
				 :custom-class="'cy-search__right--icon' + customClassRightIcon" />
		<slot />
	</view>
</template>

<script>
export default {
	name: "search",
	externalClasses: ['custom-class', 'custom-class-left-icon', 'custom-class-content', 'custom-class-input', 'custom-class-clearable', 'custom-class-action', 'custom-class-right-icon'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		leftIcon: {
			type: String,
			default: "search-line"
		},
		rightIcon: {
			type: String
		},
		value: {
			type: String
		},
		placeholder: {
			type: String,
			default: ""
		},
		action: {
			type: String,
			default: ""
		},
		shape: {
			type: String,
			default: "square"
		},
		type: {
			type: String,
			default: "text"
		},
		disabled: {
			type: Boolean,
			default: false
		},
		focus: {
			type: Boolean,
			default: false
		},
		autoBlur: {
			type: Boolean,
			default: false
		},
		holdKeyboard: {
			type: Boolean,
			default: false
		},
		clearable: {
			type: Boolean,
			default: true
		},
		confirmType: {
			type: String,
			default: "search"
		},
		placeholderStyle: String,
		placeholderClass: {
			type: String,
			default: "input-placeholder"
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassLeftIcon: {
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
		customClassAction: {
			type: [String, Array],
			default: ''
		},
		customClassClearable: {
			type: [String, Array],
			default: ''
		},
		customClassRightIcon: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {
			keyword: '',
			focused: this.focus,
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
	methods: {
		onInput(e) {
			this.keyword = e.detail.value;
			this.$emit('change', e);
		},
		handleClear() {
			this.keyword = '';
			// 延后发出事件，避免在父组件监听clear事件时，value为更新前的值(不为空)
			this.$nextTick(() => {
				this.$emit('clear');
			})
		},
		onActionClick() {
			this.$emit('action-click', this.keyword);
			try {
				// 收起键盘
				uni.hideKeyboard();
			} catch (e) { }
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
			this.$emit('submit', e.detail.value);
			try {
				// 收起键盘
				uni.hideKeyboard();
			} catch (e) { }
		},
		// 点击搜索框，只有disabled=true时才发出事件，因为禁止了输入，意味着想跳转搜索页
		clickHandler() {
			if (this.disabled) this.$emit('click');
		},
	},
} 
</script>

<style lang="scss">
@import './search.scss';
</style>