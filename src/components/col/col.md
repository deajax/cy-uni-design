## 代码演示

#### 基础

```vue
<cy-row>
  <cy-col span="8">col-8</cy-col>
  <cy-col span="8">col-8</cy-col>
  <cy-col span="8">col-8</cy-col>
</cy-row>

<cy-row>
  <cy-col span="4">col-4</cy-col>
  <cy-col span="16" offset="4">col-16 col-offsecy-4</cy-col>
</cy-row>

<cy-row>
  <cy-col offset="12" span="12">col-12 col-offsecy-12</cy-col>
</cy-row>
```

#### 增加间距

```vue
<cy-row gutter="16">
  <cy-col span="8">
    <view>col-8</view>
  </cy-col>
  <cy-col span="8">
    <view>col-8</view>
  </cy-col>
  <cy-col span="8">
    <view>col-8</view>
  </cy-col>
</cy-row>
```

## API

### 声明

| 名称   | 类型          | 默认值 | 说明                     | 必传 |
| :----- | :------------ | :----- | :----------------------- | :--- |
| span   | String/Number | -      | 列的宽度（默认单位px）   | N    |
| offset | String/Number | 0      | 列的偏移量（默认单位px） | N    |

### 插槽

| 名称    | 描述     |
| ------- | -------- |
| default | 默认插槽 |

### 外部样式类

| 类名        | 说明         |
| ----------- | ------------ |
| customClass | 根节点样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |