## 代码演示

#### 瀑布流

```vue
<cy-waterfall>
  <cy-waterfall-item v-for="i in 15" :key="i"
                     image="https://via.placeholder.com/180"
                     :title="i % 3 != 0 ? '商品标题' : '商品标题商品标题商品标题商品标题商品标题'"
                     description="描述信息"
                     price="2.00"
                     origin-price="3.00"
                     unit="盒350g">
    <view class="">slot</view>
    <view class="" slot="extra">extra</view>
  </cy-waterfall-item>
</cy-waterfall>
```

## API

### 声明

| 名称         | 类型          | 默认值      | 说明             | 必传 |
| ------------ | ------------- | ----------- | ---------------- | ---- |
| image        | String        | -           | 商品图片         | N    |
| title        | String        | -           | 商品标题         | N    |
| description  | String        | -           | 商品描述         | N    |
| price        | String/Number | -           | 价格             | N    |
| origin-price | String/Number | -           | 划线价格         | N    |
| url          | String        | -           | 点击后的跳转链接 |      |
| jump-type    | String        | navigate-to | 链接跳转类型     |      |

### 插槽

| 名称    | 描述         |
| ------- | ------------ |
| default | 内容区域插槽 |
| extra   | 底部区域插槽 |

### 事件

| 名称   | 参数 | 描述       |
| ------ | ---- | ---------- |
| @click | -    | 点击时触发 |

### 外部样式类

| 类名         | 说明 |
| ------------ | ---- |
| custom-class |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |