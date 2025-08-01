<template>
	<view :class="['cy-empty', customClass]">
		<view class="cy-empty__thumb">
			<template v-if="image">
				<image
					:class="['cy-empty__thumb--image', customClassImage]"
					:style="customStyleImage"
					:src="
						image === 'list'
							? empty.list
							: image === 'search'
							? empty.search
							: image === 'network'
							? empty.network
							: image === 'item'
							? empty.item
							: image === 'default'
							? empty.default
							: image
					"
					mode="widthFix"
				/>
			</template>
			<slot v-else name="image" />
			<cy-icon v-if="icon" :custom-class="'cy-empty__thumb--icon ' + customClassIcon" :name="icon.name || icon" :color="icon.color || ''" :size="icon.size || '64'" />

			<slot v-else name="icon" />
		</view>
		<view :class="['cy-empty__description', customClassDescription]" v-if="description || $slots.description">
			{{ description }}
			<slot name="description" />
		</view>
		<view :class="['cy-empty__actions', customClassActions]" v-if="$slots.action">
			<slot name="action" />
		</view>
	</view>
</template>

<script>
export default {
	name: 'empty',
	externalClasses: ['custom-class', 'custom-class-description', 'custom-class-image', 'custom-class-icon', 'custom-class-actions', 'custom-style-image'],
	options: {
		styleIsolation: 'shared',
		addGlobalClass: true,
		virtualHost: true,
		externalClasses: true
	},
	props: {
		image: {
			type: String,
			default: ''
		},
		icon: [String, Object],
		description: {
			type: String,
			default: '暂无内容'
		},

		// externalClasses
		customClass: {
			type: [String, Array],
			default: ''
		},
		customClassImage: {
			type: [String, Array],
			default: ''
		},
		customClassIcon: {
			type: [String, Array],
			default: ''
		},
		customClassDescription: {
			type: [String, Array],
			default: ''
		},
		customClassActions: {
			type: [String, Array],
			default: ''
		},
		// externalStyles
		customStyleImage: {
			type: [String, Object],
			default: ''
		},
	},
	data() {
		return {
			empty: {
				default: 'https://cy-static-resources.oss-cn-beijing.aliyuncs.com/retailshop/img/empty-state_default.png',
				search: 'https://cy-static-resources.oss-cn-beijing.aliyuncs.com/retailshop/img/empty-state_search.png',
				network: 'https://cy-static-resources.oss-cn-beijing.aliyuncs.com/retailshop/img/empty-state_network.png',
				list: 'https://cy-static-resources.oss-cn-beijing.aliyuncs.com/retailshop/img/empty-state_list.png',
				item: 'https://cy-static-resources.oss-cn-beijing.aliyuncs.com/retailshop/img/empty-state_item.png'
			}
		};
	}
};
</script>

<style lang="scss">
@import './empty.scss';
</style>
