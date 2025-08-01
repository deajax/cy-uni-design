<template>
	<button :class="['cy-goods-action-icon', disabled ? 'cy-goods-action-icon--disabled' : '', customClass]"
		  hover-class="cy-goods-action-icon--hover"
		  hover-stay-time="70"
		  :disabled="disabled"
          :open-type="openType"
		  @click="handleTap">
		<cy-badge :count="badge" v-if="badge && badge > 0">
			<cy-icon :name="icon" size="40" :custom-class="customClassIcon" />
		</cy-badge>
		<cy-icon v-else :name="icon" size="40" :custom-class="customClassIcon" />
		<text>{{ text }}</text>
		<slot />
	</button>
</template>

<script>
export default {
	name: "goods-action-icon",
	externalClasses: ['custom-class', 'custom-class-icon'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		icon: {
			type: String,
		},
		text: {
			type: String,
		},
		badge: {
			type: [String, Number],
		},
        openType: {
            type: String,
        },
		disabled: {
			type: Boolean,
			default: false
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassIcon: {
			type: [String, Array],
			default: ''
		},
	},
	data() {
		return {}
	},
	computed: {},
	methods: {
		handleTap(event) {
			this.$emit('click', event);
		}
	},
} 
</script>

<style lang="scss">
@import './goods-action-icon.scss';
</style>