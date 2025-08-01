<template>
	<div class="cell">
		<cy-cell-group title="title">
			<cy-cell title="单行标题" note="辅助信息" arrow />

			<cy-cell left-icon="home-4-line" title="单行标题" note="辅助信息" arrow>
				<view class="" slot="left-icon">22</view>
			</cy-cell>

			<cy-cell title="单行标题" note="辅助信息" required>
				<view class="" slot="left-icon">22</view>
				<view class="" slot="right-icon">
					<cy-icon name="home-4-line" :size="40" />
				</view>
			</cy-cell>
		</cy-cell-group>

		<cy-cell-group title="卡片单元格" theme="card">
			<view slot="extra">slot额外内容</view>

			<cy-cell left-icon="function-line" title="单行标题" note="辅助信息" arrow />

			<cy-cell left-icon="home-4-line" title="单行标题" description="一段很长很长的内容文字" note="辅助信息" arrow />

			<cy-cell title="单行标题">
				<view class="" slot="description">一段很长很长的内容文字，长文本自动换行，该选项的描述是一段很长的内容</view>
			</cy-cell>

			<cy-cell image="https://via.placeholder.com/80" title="单行标题" description="一段很长很长的内容文字" />
		</cy-cell-group>
	</div>
</template>

<script>
export default {
	data() {
		return {}
	}
}
</script>

<style lang="scss">
page {
	background: #f5f5f5;
}
</style>