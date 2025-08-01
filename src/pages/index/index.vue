<template>
	<view class="content cy-safe-area-bottom">
		<cy-cell-group :title="group.title" v-for="(group, index) in menu" :key="index">
			<template>
				<cy-cell v-for="(item, i) in group.children" :title="item.title" :note="item.note" :url="item.url"
						 :key="i" arrow />
			</template>
		</cy-cell-group>
	</view>
</template>

<script>
export default {
	data() {
		return {
			menu: [{
				title: "基础",
				children: [
					{ title: "Button 按钮", url: "/pages/button/button" },
					{ title: "Divider 分割线", url: "/pages/divider/divider" },
					{ title: "Fab 悬浮按钮", url: "/pages/fab/fab" },
					{ title: "Gap 间隔", url: "/pages/gap/gap" },
					{ title: "Icon 图标", url: "/pages/icon/icon" },
					{ title: "Layout 布局", url: "/pages/layout/layout" },
					{ title: "Text 文本", url: "/pages/text/text" },
				]
			}, {
				title: "导航",
				children: [
					{ title: "Navbar 导航栏", url: "/pages/navbar/navbar" },
					{ title: "GoodsAction 商品导航", url: "/pages/goods-action/goods-action" },
					{ title: "SubmitBar 提交订单栏", url: "/pages/submit-bar/submit-bar" },
					{ title: "Tabs 选项卡", url: "/pages/tabs/tabs" },
				]
			}, {
				title: "输入",
				children: [
					{ title: "Input 输入框", url: "/pages/input/input" },
					{ title: "Checkbox 多选框", url: "/pages/checkbox/checkbox" },
					{ title: "Radio 单选框", url: "/pages/radio/radio" },
					{ title: "Search 搜索框", url: "/pages/search/search" },
					{ title: "Stepper 步进器", url: "/pages/stepper/stepper" },
					{ title: "Textarea 多行文本框", note: "", url: "/pages/textarea/textarea" },
					{ title: "Upload 上传", url: "/pages/upload/upload" },
				]
			}, {
				title: "数据展示",
				children: [
					{ title: "Avatar 头像", url: "/pages/avatar/avatar" },
					{ title: "Badge 徽标", url: "/pages/badge/badge" },
					{ title: "Card 卡片", url: "/pages/card/card" },
					{ title: "Cell 单元格", url: "/pages/cell/cell" },
					{ title: "Empty 空状态", url: "/pages/empty/empty" },
					{ title: "Grid 宫格", url: "/pages/grid/grid" },
					{ title: "Price 价格", url: "/pages/price/price" },
					{ title: "Sticky 吸顶", url: "/pages/sticky/sticky" },
					{ title: "Tag 标签", url: "/pages/tag/tag" },
				]
			}, {
				title: "反馈",
				children: [
					{ title: "Dialog 对话框", url: "/pages/dialog/dialog" },
					{ title: "Loading 加载", url: "/pages/loading/loading" },
					{ title: "Message 消息通知", url: "/pages/message/message" },
					{ title: "NoticeBar 公告栏", url: "/pages/notice-bar/notice-bar" },
					{ title: "Popup 弹出层", url: "/pages/popup/popup" },
					{ title: "Popover 气泡弹出框", url: "/pages/popover/popover" },
					{ title: "Result 结果", url: "/pages/result/result" },
				]
			}, {
				title: "业务组件",
				children: [
					{ title: "GoodsItem 商品", url: "/pages/goods-item/goods-item" },
					{ title: "Waterfall 瀑布流", url: "/pages/waterfall/waterfall" },
				]
			}]
		}
	},
	onLoad() {
		var version = 'V1.0.0';
		console.log(
			'  ______    __  __    ______    __   __    ______     __  __    __    \r\n',
			'/\\  ___\\  /\\ \\_\\ \\  /\\  ___\\  /\\ "-.\\ \\  /\\  ___\\   /\\ \\_\\ \\  /\\ \\   \r\n',
			'\\ \\ \\____ \\ \\  __ \\ \\ \\  __\\  \\ \\ \\-.  \\ \\ \\ \\__ \\  \\ \\____ \\ \\ \\ \\  \r\n',
			' \\ \\_____\\ \\ \\_\\ \\_\\ \\ \\_____\\ \\ \\_\\\\"\\_\\ \\ \\_____\\  \\/\\_____\\ \\ \\_\\ \r\n',
			'  \\/_____/  \\/_/\\/_/  \\/_____/  \\/_/ \\/_/  \\/_____/   \\/_____/  \\/_/ \r\n',
			'\r\n',
			'-------------------------- 诚驿uniapp组件库 --------------------------'
		);
		console.log(
			`%c CY Design %c ${version} %c`,
			`background:#1890ff; border:1px solid #1890ff; padding:1px; color:#fff;`,
			`border:1px solid #1890ff; padding:1px; color:#1890ff;`,
			'background:transparent',
		);
	}
}
</script>

<style lang="scss">
page {
	background: #f5f5f5;
}
</style>