<template>
  <view class="message">
    <cy-message icon="information-fill" theme="info" content='这是一条普通通知信息' :link="{ content: '按钮' }" closeBtn />

    <cy-message theme="success" content='这是一条成功的提示消息' :link="{ content: '按钮' }" closeBtn
                :custom-style="{ top: '80px' }" />

    <cy-message theme="warning" content='这是一条需要用户关注到的警示通知通知通知通知' :link="{ content: '按钮' }" closeBtn
                :custom-style="{ top: '144px' }" />

    <cy-message theme="error" content='这是一条错误提示通知' :link="{ content: '按钮' }" closeBtn
                :custom-style="{ top: '232px' }" />
  </view>
</template>

<script>
export default {
  components: {},
  data() {
    return {}
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
page {
  background: #f5f5f5;
}
</style>