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

### 插槽

| 名称    | 描述     |
| ------- | -------- |
| default | 内容插槽 |

### 外部样式类

| 类名         | 说明         |
| ------------ | ------------ |
| custom-class | 跟节点样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |