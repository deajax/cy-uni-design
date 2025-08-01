<script>
export default {
	onLaunch: function () {
		console.log('App Launch')
	},
	onShow: function () {
		console.log('App Show')
	},
	onHide: function () {
		console.log('App Hide')
	}
}
</script>

<style lang="scss">
/*每个页面公共css */
@import "@/components/common/index.scss";

/* #ifdef MP-ALIPAY */
page {
	background: #fff;
}
/* #endif */

.title {
	padding: 0 16px;
	line-height: 48px;
	opacity: .35;
}

.example {
	margin-bottom: 16px;
}

.flex {
	display: flex;
	align-items: center;
}

.flex-col {
	flex-direction: column;
}

.code {
	padding: 16px;
	background: #f0f0f0;
}
</style>
