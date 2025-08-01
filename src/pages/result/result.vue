<template>
  <view class="result">
    <view class="example">
      <cy-result
        status="success"
        title="支付成功"
        description="您已享受会员折扣优惠"
      >
        <template #extra>
          <cy-button theme="primary">Go Console</cy-button>
          <text style="padding: 4px" />
          <cy-button>Buy Again</cy-button>
        </template>
      </cy-result>
    </view>

    <view class="example">
      <cy-result
        status="info"
        title="Your operation has been executed"
      >
        <template #extra>
          <cy-button theme="primary">Go Console</cy-button>
        </template>
      </cy-result>
    </view>

    <view class="example">
      <cy-result
        status="warning"
        title="There are some problems with your operation."
      >
        <template #extra>
          <cy-button theme="primary">Go Console</cy-button>
        </template>
      </cy-result>
    </view>

    <view class="example">
      <cy-result
        status="error"
        title="Submission Failed"
        description="Your account has been frozen"
      >
        <template #extra>
          <cy-button theme="primary">Go Console</cy-button>
          <text style="padding: 4px" />
          <cy-button>Buy Again</cy-button>
        </template>
      </cy-result>
    </view>
  </view>
</template>

<script>
export default {
  components: {},
  data() {
    return {};
  },
  computed: {},
  methods: {},
  watch: {},

  // 页面周期函数--监听页面加载
  onLoad() {},
  // 页面周期函数--监听页面初次渲染完成
  onReady() {},
  // 页面周期函数--监听页面显示(not-nvue)
  onShow() {},
  // 页面周期函数--监听页面隐藏
  onHide() {},
  // 页面周期函数--监听页面卸载
  onUnload() {},
  // 页面处理函数--监听用户下拉动作
  // onPullDownRefresh() { uni.stopPullDownRefresh(); },
  // 页面处理函数--监听用户上拉触底
  // onReachBottom() {},
  // 页面处理函数--监听页面滚动(not-nvue)
  // onPageScroll(event) {},
  // 页面处理函数--用户点击右上角分享
  // onShareAppMessage(options) {},
};
</script>

<style lang="scss">
page {
  background: #f5f5f5;
}
</style>
