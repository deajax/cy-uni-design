## 代码演示

#### 基础用法

```vue
<cy-goods-item image="https://via.placeholder.com/180"
    title="Apple/苹果 iPhone 15 128GB 黑色"
    description="企业新客限时专享补贴3000元，更有企业团购低至85折！"
    price="4899.00"
    origin-price="5199.00"
    v-for="i in 2" :key="i">
  <cy-button theme="primary" icon="add-line" size="extra-small" shape="circle" slot="action" />
  <view class="">slot</view>
  <view class="" slot="extra">extra</view>
</cy-goods-item>
```

#### 纵向布局

```vue
<scroll-view scroll-x>
  <view style="display:flex; gap:12px; flex-wrap:nowrap; width:fit-content; padding:0 16px;">
    <view v-for="i in 6" :key="i" style="width:160px; display:inline-block;">
      <cy-goods-item image="https://via.placeholder.com/180"
                     title="商品标题"
                     description="描述信息"
                     price="2.00"
                     origin-price="3.00"
                     layout="vertical">
        <cy-button icon="add-line" size="extra-small" shape="circle" slot="action" />
      </cy-goods-item>
    </view>
  </view>
</scroll-view>
```

#### 圆角

```vue
<view class="example" style="padding: 0 16px;">
  <cy-goods-item image="https://via.placeholder.com/180"
                 title="商品标题"
                 description="描述信息"
                 price="2.00"
                 origin-price="3.00"
                 unit="盒350g"
                 round>
    <cy-button icon="add-line" size="extra-small" shape="circle" slot="action" />
    <view class="baokuan">爆款</view>
    <view class="extra" slot="extra">
      <cy-tag size="small" variant="light" theme="danger">包邮</cy-tag>
      <cy-tag size="small" variant="light" theme="primary">满5000减300</cy-tag>
    </view>
  </cy-goods-item>
</view>
```

## API

### 声明

| 名称        | 类型           | 默认值     | 说明                                                         | 必传 |
| ----------- | -------------- | ---------- | ------------------------------------------------------------ | ---- |
| layout      | String         | horizontal | 布局模式，可选值`vertical`                                   | N    |
| image       | String         | -          | 主图                                                         | N    |
| title       | String         | -          | 标题                                                         | N    |
| description | String         | -          | 下方内容描述                                                 | N    |
| price       | String｜Number | -          | 价格                                                         | N    |
| originPrice | String｜Number | -          | 划线价格                                                     | N    |
| unit        | String         | -          | 单位                                                         | N    |
| round       | Boolean        | false      | 是否为圆角                                                   | N    |
| hover       | Boolean        | true       | 是否开启点击反馈                                             | N    |
| bordered    | Boolean        | true       | 是否显示边框                                                 | N    |
| url         | String         | -          | 点击后跳转链接地址。如果值为空，则表示不需要跳转             | N    |
| jumpType    | String         | navigateTo | 链接跳转类型。可选项：switchTab/reLaunch/redirectTo/navigateTo | N    |

### 插槽

| 名称        | 描述               |
| ----------- | ------------------ |
| default     | 默认插槽，标题下方 |
| image       | 主图上方           |
| title       | 标题下方           |
| description | 描述下方           |
| originPrice | 划线价格下方       |
| price       | 价格下方           |
| action      | 操作栏             |
| extra       | 文本下方额外内容   |

### 事件

| 名称   | 参数    | 描述 |
| ------ | ------- | ---- |
| @click | `event` | -    |

### 外部样式类

| 类名                   | 说明           |
| ---------------------- | -------------- |
| customClass            | 根节点样式类   |
| customClassImage       | 主图样式类     |
| customClassContent     | 内容样式类     |
| customClassTitle       | 标题样式类     |
| customClassDescription | 描述样式类     |
| customClassNote        | 文本样式类     |
| customClassPrice       | 价格样式类     |
| customClassOriginPrice | 划线价格样式类 |
| customClassAction      | 操作栏样式类   |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                                     | 默认值          | 描述 |
| ---------------------------------------- | --------------- | ---- |
| --cy-goods-item-round                    | $radius-default | -    |
| --cy-goods-item-horizontal-padding       | $spacer-2       | -    |
| --cy-goods-item-border-left-space        | 32rpx           | -    |
| --cy-goods-item-horizontal-image-size    | 176rpx          | -    |
| --cy-goods-item-horizontal-image-round   | $radius-default | -    |
| --cy-goods-item-vertical-round           | $radius-default | -    |
| --cy-goods-item-vertical-content-padding | $spacer-1       | -    |
| --cy-goods-item-vertical-title-font-size | $font-size-base | -    |
| --cy-goods-item-title-font-size          | $font-size-base | -    |
| --cy-goods-item-description-font-size    | $font-size-s    | -    |
| --cy-goods-item-description-color        | $font-gray-3    | -    |
| --cy-goods-item-origin-price-font-size   | $font-size-s    | -    |