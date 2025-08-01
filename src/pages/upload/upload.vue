<template>
	<view class="upload" style="padding-bottom: 80px;">
		<view class="title">只选择图片</view>
		<view class="wrapper">
			<cy-upload v-model="value" limit="9" :source-type="sourceType" />
		</view>

		<view class="title">只选择视频</view>
		<view class="wrapper">
			<cy-upload v-model="value" limit="9" media-type="video" :source-type="sourceType" />
		</view>

		<view class="title">组件状态</view>
		<view class="wrapper">
			<cy-upload v-model="status" limit="9" :source-type="sourceType" />
		</view>

		<view class="title">自定义来源</view>
		<view class="wrapper">
			<cy-upload limit="9" title="从相册选图" :source-type="['album']" />
		</view>
		<view class="wrapper">
			<cy-upload limit="9" title="使用相机" media-type="video" :source-type="['camera']" />
		</view>

		<view class="title">组件标题</view>
		<view class="wrapper">
			<cy-upload title="最多选择9张图片" />
		</view>

		<view class="title">自定义上传按钮</view>
		<view class="wrapper">
			<cy-upload media-type="image">
				<cy-icon name="share-2-line" />
			</cy-upload>
		</view>
		<view class="wrapper">
			<cy-upload media-type="video">
				<cy-button size="small">自定义按钮</cy-button>
			</cy-upload>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			sourceType: ['album', 'camera'],
			status: [{
				"name": "loading.jpg",
				"extname": "jpg",
				"url": "",
				"status": 'loading',
				"progress": -1
			}, {
				"name": "progress.jpg",
				"extname": "jpg",
				"url": "",
				"status": 'progress',
				"progress": 68
			}, {
				"name": "error.jpg",
				"extname": "jpg",
				"url": "",
				"status": 'error'
			}],
		}
	},
	methods: {

	}
}
</script>

<style lang="scss">
page {
	background: #f5f5f5;
}

.wrapper {
	padding: 16px;
	margin-bottom: 16px;
}
</style>