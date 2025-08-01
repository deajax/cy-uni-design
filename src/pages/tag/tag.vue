<template>
  <div class="tag">
    <view class="title">组件类型</view>
    <view class="example">
      <view class="example-desc">基础标签</view>

      <cy-tag variant="light">标签文字</cy-tag>
      <cy-tag variant="outline">标签文字</cy-tag>
    </view>

    <view class="example">
      <view class="example-desc">圆弧标签</view>
      <cy-tag variant="light" shape="round">标签文字</cy-tag>
      <cy-tag variant="outline" shape="round">标签文字</cy-tag>
      <cy-tag variant="outline" shape="mark">标签文字</cy-tag>
    </view>

    <view class="example">
      <view class="example-desc">带图标的标签</view>
      <cy-tag variant="light" icon="information-line"> 标签文字 </cy-tag>
      <cy-tag variant="outline" icon="information-line"> 标签文字 </cy-tag>
      <cy-tag variant="outline" :icon="{ name: 'information-line', color: 'red', size: '24' }"> 标签文字 </cy-tag>
    </view>

    <view class="example">
      <view class="example-desc">超长省略文本标签</view>
      <cy-tag max-width="130" variant="light">超长省略文本标签超长省略文本标签</cy-tag>
    </view>

    <view class="title">可关闭的标签</view>
    <view class="example">
      <cy-tag @close="handleClose0" closable variant="light">文字标签</cy-tag>
      <cy-tag @close="handleClose1" closable variant="outline">文字标签</cy-tag>
    </view>

    <view class="title">组件状态</view>
    <view class="example">
      <cy-tag variant="light">默认</cy-tag>
      <cy-tag variant="light" theme="primary">主要</cy-tag>
      <cy-tag variant="light" theme="warning">警告</cy-tag>
      <cy-tag variant="light" theme="danger">危险</cy-tag>
      <cy-tag variant="light" theme="success">成功</cy-tag>
    </view>

    <view class="example">
      <cy-tag theme="default">默认</cy-tag>
      <cy-tag theme="primary">主要</cy-tag>
      <cy-tag theme="warning">警告</cy-tag>
      <cy-tag theme="danger">危险</cy-tag>
      <cy-tag theme="success">成功</cy-tag>
    </view>

    <view class="example">
      <cy-tag variant="outline">默认</cy-tag>
      <cy-tag variant="outline" theme="primary">主要</cy-tag>
      <cy-tag variant="outline" theme="warning">警告</cy-tag>
      <cy-tag variant="outline" theme="danger">危险</cy-tag>
      <cy-tag variant="outline" theme="success">成功</cy-tag>
    </view>

    <view class="example">
      <cy-tag variant="light-outline">默认</cy-tag>
      <cy-tag variant="light-outline" theme="primary">主要</cy-tag>
      <cy-tag variant="light-outline" theme="warning">警告</cy-tag>
      <cy-tag variant="light-outline" theme="danger">危险</cy-tag>
      <cy-tag variant="light-outline" theme="success">成功</cy-tag>
    </view>

    <view class="title">组件尺寸</view>
    <view class="example">
      <cy-tag class="margin-8" size="extra-large" variant="light" closable>加大尺寸</cy-tag>
      <cy-tag class="margin-8" size="large" variant="light" closable>大尺寸</cy-tag>
      <cy-tag class="margin-8" size="medium" variant="light" closable>中尺寸</cy-tag>
      <cy-tag class="margin-8" size="small" variant="light" closable>小尺寸</cy-tag>
    </view>

  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      items: ['light', 'dark', 'outline', 'light-outline']
    }
  },
  computed: {},
  methods: {},
  watch: {},

  // 页面周期函数--监听页面加载
  onLoad() { },
  // 页面周期函数--监听页面初次渲染完成
  onReady() { },
  // 页面周期函数--监听页面显示(not-nvue)
  onShow() { },
  // 页面周期函数--监听页面隐藏
  onHide() { },
  // 页面周期函数--监听页面卸载
  onUnload() { },
  // 页面处理函数--监听用户下拉动作
  // onPullDownRefresh() { uni.stopPullDownRefresh(); },
  // 页面处理函数--监听用户上拉触底
  // onReachBottom() {},
  // 页面处理函数--监听页面滚动(not-nvue)
  // onPageScroll(event) {},
  // 页面处理函数--用户点击右上角分享
  // onShareAppMessage(options) {},
} 
</script>

<style lang="scss">
.example {
	padding: 0 16px;
  display: flex;
  flex-wrap: wrap;
  column-gap: 8px;
}

.example-desc {
  width: 100%;
  font-size: 12px;
  margin-bottom: 12px;
  color: gray;
}
</style>