## 代码演示

#### 列间隔

```vue
<cy-gap gutter="8">
  <cy-tag variant="light">标签文字</cy-tag>
  <cy-tag variant="outline">标签文字</cy-tag>
  <cy-tag variant="outline">标签文字</cy-tag>
</cy-gap>
```

#### 行间隔和列间隔

```vue
<cy-gap :gutter="[8, 16]">
	<cy-tag variant="outline" v-for="i in 12" :key="i">标签文字</cy-tag>
</cy-gap>
```

#### 纵向布局

```vue
<cy-gap layout="vertical" :gutter="[0, 8]">
  <cy-button variant="outline" block>填充按钮</cy-button>
  <cy-button variant="outline" block>填充按钮</cy-button>
  <cy-button variant="outline" block>填充按钮</cy-button>
</cy-gap>
```



## API

### 声明

| 名称   | 类型         | 默认值     | 说明                                                         | 必传 |
| :----- | :----------- | :--------- | :----------------------------------------------------------- | :--- |
| layout | String       | horizontal | 布局方向，可选`vertical`                                     | N    |
| gutter | Array/String | 4          | 间隔尺寸，固定单位为`px`，设置String类型为水平间隔，或者使用数组形式同时设置 `[水平间距, 垂直间距]` | N    |

### 插槽

| 名称    | 描述         |
| :------ | :----------- |
| default | 默认内容插槽 |

### 外部样式类

| 类名         | 说明         |
| :----------- | :----------- |
| custom-class | 根节点样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| :--- | :----- | :--- |
|      |        |      |