## 代码演示

#### 基础提交栏

```vue
<cy-submit-bar>
  <template #left>
		solt
  </template>
  <template #description>
		共3件商品，已优惠¥1.00
  </template>
</cy-submit-bar>
```



## API

### 声明

| 名称                   | 类型            | 默认值     | 说明                            | 必传 |
| ---------------------- | --------------- | ---------- | ------------------------------- | ---- |
| safe-area-inset-bottom | Boolean         | true       | 是否为 iPhoneX 留出底部安全距离 | N    |
| price                  | Number / String | 0          | 价格展示                        | N    |
| button-text            | String          | '提交订单' | 提交按钮文字                    | N    |
| disabled               | Boolean         | false      | 是否禁用提交按钮                | N    |

### 插槽

| 名称        | 描述         |
| ----------- | ------------ |
| left        | 左侧区域     |
| description | 价格说明区域 |
| button      | 提交按钮区域 |

### 事件

| 名称    | 参数 | 描述     |
| ------- | ---- | -------- |
| @submit | e    | 提交事件 |

### 外部样式类

| 类名                   | 说明 |
| ---------------------- | ---- |
| customClass            |      |
| customClassContent     |      |
| customClassActions     |      |
| customClassLeft        |      |
| customClassCurrency    |      |
| customClassPrice       |      |
| customClassDescription |      |
| customClassButton      |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |