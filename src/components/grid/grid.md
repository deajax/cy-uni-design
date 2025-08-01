## 代码演示

#### 基础宫格

```vue
<cy-grid class="block" :column="5">
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="最多四字" :image="img" />
</cy-grid>

<cy-grid class="block">
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="最多五个字" :image="img" />
</cy-grid>

<cy-grid class="block" :column="3">
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="最多六个文字" :image="img" />
</cy-grid>
```

```javascript
<script>
export default {
	data() {
		return {
			img: 'https://via.placeholder.com/80',
		}
	}
} 
</script>
```



#### 带说明的宫格

```vue
<view class="block">
  <cy-grid column="3">
    <cy-grid-item text="标题文字" description="描述文字" :image="img" />
    <cy-grid-item text="标题文字" description="描述文字" :image="img" />
    <cy-grid-item text="标题文字" description="描述文字" :image="img" />
  </cy-grid>
</view>

<view class="block">
  <cy-grid column="2" align="left">
    <cy-grid-item text="标题文字" description="描述文字" layout="horizontal" :image="img" />
    <cy-grid-item text="标题文字" description="描述文字" layout="horizontal" :image="img" />
  </cy-grid>
</view>
```

#### 带边框的宫格

```vue
<view class="block">
  <cy-grid bordered column="3">
    <cy-grid-item text="标题文字" :image="img" />
    <cy-grid-item text="标题文字" :image="img" />
    <cy-grid-item text="标题文字" :image="img" />
  </cy-grid>
</view>

<view class="block">
  <cy-grid bordered column="2" align="left">
    <cy-grid-item text="标题文字" description="描述文字" layout="horizontal" :image="img" />
    <cy-grid-item text="标题最多六字" description="描述文字" layout="horizontal" :image="img" />
  </cy-grid>
</view>
```

#### 带徽章的宫格

```
<cy-grid class="cy-grid badge">
  <cy-grid-item text="标题文字" :image="img" :badge-props="{ dot: true }" />
  <cy-grid-item text="标题文字" :image="img" :badge-props="{ count: 8 }" />
  <cy-grid-item text="标题文字" :image="img" :badge-props="{ count: 13 }" />
  <cy-grid-item text="标题文字" :image="img" :badge-props="{ count: 'NEW' }" />
</cy-grid>
```

#### 可滑动的宫格

```vue
<cy-grid class="block" column="0">
  <cy-grid-item v-for="i in 8" :key="i" text="最多五个字" :image="img" />
</cy-grid>
```

#### 可传图标的宫格

```vue
<cy-grid class="block">
  <cy-grid-item text="分享" icon="share-line" bindclick="onClick" />
  <cy-grid-item text="收藏" icon="star-line" bindclick="onClick" />
  <cy-grid-item text="保存" icon="import-line" bindclick="onClick" />
  <cy-grid-item text="编辑" icon="draft-line" bindclick="onClick" />
</cy-grid>
```

#### 多行宫格

```vue
<cy-grid class="block" column="4">
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="最多五个字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="最多五个字" :image="img" />
</cy-grid>
```

#### 卡片宫格

```vue
<cy-grid class="block" column="4" theme="card">
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="最多五个字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="标题文字" :image="img" />
  <cy-grid-item text="最多五个字" :image="img" />
</cy-grid>
```

## API

### 声明

| 名称      | 类型             | 默认值  | 说明                                                         | 必传 |
| :-------- | :--------------- | :------ | :----------------------------------------------------------- | :--- |
| align     | String           | center  | 内容对齐方式。可选项：left/center                            | N    |
| border    | Boolean / Object | false   | 边框，默认不显示。值为 true 则显示默认边框，值类型为 object 则表示自定义边框样式。 | N    |
| column    | Number           | 4       | 每一行的列数量；为 0 时等于固定大小                          | N    |
| gutter    | Number           | -       | 间隔大小                                                     | N    |
| hover     | Boolean          | false   | 是否开启点击反馈                                             | N    |
| theme     | String           | default | 宫格的风格。可选项：default/card                             | N    |
| indicator | Boolean          | true    | 滑动宫格的滚动条，仅在开启滑动宫格的情况下显示               | N    |

### 插槽

| 名称    | 描述     |
| ------- | -------- |
| default | 默认插槽 |

### 外部样式类

| 类名               | 说明           |
| ------------------ | -------------- |
| customClass        | 根节点样式类   |
| customClassContent | 内容节点样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |