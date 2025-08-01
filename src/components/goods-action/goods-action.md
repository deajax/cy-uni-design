## 代码演示

#### 基础演示

```vue
<goods-action @add-cart="addCart" @buy-now="buyNow">
  <goods-action-icon icon="customer-service-line" text="客服" />
  <goods-action-icon icon="shopping-cart-2-line" text="购物车" />
</goods-action>
```

## API

### 声明

| 名称                   | 类型    | 默认值 | 说明                   | 必传 |
| ---------------------- | ------- | ------ | ---------------------- | ---- |
| add-cart-btn           | Boolean | true   | 是否显示加入购物车按钮 | N    |
| buy-now-btn            | Boolean | true   | 是否显示立即购买按钮   | N    |
| safe-area-inset-bottom | Boolean | true   | 是否启用底部安全区域   | N    |

### 插槽

| 名称    | 描述         |
| ------- | ------------ |
| default | 左侧图标内容 |
| content | 左侧内容     |
| action  | 右侧内容     |

### 事件

| 名称      | 参数    | 描述 |
| --------- | ------- | ---- |
| @add-cart | `event` | -    |
| @buy-now  | `event` | -    |

### 外部样式类

| 类名               | 说明           |
| ------------------ | -------------- |
| customClass        | 根节点样式类   |
| customClassContent | 内容部分样式类 |
| customClassIcon    | 图标区域样式类 |
| customClassAction  | 操作区域样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                                    | 默认值       | 描述 |
| --------------------------------------- | ------------ | ---- |
| --cy-goods-action-content-padding       | 12rpx        | -    |
| --cy-goods-action-actions-padding       | 0 $spacer    | -    |
| --cy-goods-action-description-font-size | $font-size   | -    |
| --cy-goods-action-description-color     | $font-gray-2 | -    |
| --cy-goods-action-placeholder-size      | 104rpx       | -    |