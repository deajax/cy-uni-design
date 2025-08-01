## 代码演示

### 类型

```
<cy-cell title="单行标题" note="辅助信息" arrow />

<cy-cell left-icon="home-4-line" title="单行标题" note="辅助信息" arrow>
	<view slot="left-icon">22</view>
</cy-cell>

<cy-cell title="单行标题" note="辅助信息" required>
  <view class="" slot="left-icon">22</view>
  <view class="" slot="right-icon">
    <cy-icon name="home-4-line" :size="40" />
  </view>
</cy-cell>
```

#### 卡片单元格

```
<cy-cell-group title="卡片单元格" theme="card">
  <view slot="extra">slot额外内容</view>
  <cy-cell left-icon="function-line" title="单行标题" note="辅助信息" arrow />
  <cy-cell left-icon="home-4-line" title="单行标题" description="一段很长很长的内容文字" note="辅助信息" arrow />
  <cy-cell title="单行标题">
    <view slot="description">一段很长很长的内容文字，长文本自动换行，该选项的描述是一段很长的内容</view>
  </cy-cell>
  <cy-cell image="https://via.placeholder.com/80" title="单行标题" description="一段很长很长的内容文字" />
</cy-cell-group>
```



## API

### 声明

| 名称        | 类型                   | 默认值     | 说明                                                         | 必传 |
| :---------- | :--------------------- | :--------- | :----------------------------------------------------------- | :--- |
| align       | String                 | middle     | 内容的对齐方式，默认居中对齐。可选项：top/middle/bottom      | N    |
| arrow       | Boolean / Object       | false      | 是否显示右侧箭头                                             | N    |
| bordered    | Boolean                | true       | 是否显示下边框                                               | N    |
| description | String / Slot          | -          | 下方内容描述                                                 | N    |
| hover       | Boolean                | -          | 是否开启点击反馈                                             | N    |
| image       | String / Slot          | -          | 主图                                                         | N    |
| jump-type   | String                 | navigateTo | 链接跳转类型。可选项：switchTab/reLaunch/redirectTo/navigateTo | N    |
| left-icon   | String / Object / Slot | -          | 左侧图标，出现在单元格标题的左侧                             | N    |
| note        | String / Slot          | -          | 和标题同行的说明文字                                         | N    |
| required    | Boolean                | false      | 是否显示表单必填星号                                         | N    |
| right-icon  | String / Object / Slot | -          | 最右侧图标                                                   | N    |
| title       | String / Slot          | -          | 标题                                                         | N    |
| url         | String                 | -          | 点击后跳转链接地址。如果值为空，则表示不需要跳转             | N    |

### 插槽

| 名称         | 描述         |
| ------------ | ------------ |
| left-icon    | 图标后方     |
| image        | 图片后方     |
| title        | 标题后方     |
| description  | 内容描述后方 |
| note/default | 说明文字后方 |
| right-icon   | 右侧图标后方 |
| extra        | 内容描述下方 |

### 事件

| 名称   | 参数 | 描述 |
| ------ | ---- | ---- |
| @click | -    |      |

### 外部样式类

| 类名                     | 说明               |
| :----------------------- | :----------------- |
| custom-class             | 根节点样式类       |
| custom-class-title       | 标题样式类         |
| custom-class-description | 下方描述内容样式类 |
| custom-class-note        | 右侧说明文字样式类 |
| custom-class-left        | 左侧内容样式类     |
| custom-class-right       | 右侧内容样式类     |

### CellGroup

| 名称     | 类型    | 默认值  | 说明                             | 必传 |
| :------- | :------ | :------ | :------------------------------- | :--- |
| bordered | Boolean | -       | 是否显示组边框                   | N    |
| theme    | String  | default | 单元格风格。可选项：default/card | N    |
| title    | String  | -       | 单元格组标题                     | N    |

### CellGroup 插槽

| 类名   | 说明               |
| :----- | :----------------- |
| header | 整个头部，标题下面 |
| extra  | 标题右侧           |

### CellGroup 外部样式类

| 类名                 | 说明                   |
| :------------------- | :--------------------- |
| custom-class         | 根节点样式类           |
| custom-class-header  | 头部样式类             |
| custom-class-title   | 标题样式类             |
| custom-class-extra   | 标题右侧额外内容样式类 |
| custom-class-content | 内容样式类             |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                               | 默认值                       | 描述 |
| :--------------------------------- | :--------------------------- | :--- |
| --cy-cell-group-border-color       | $border-color                | -    |
| --cy-cell-group-title-bg-color     | $bg-color-secondarycontainer | -    |
| --cy-cell-group-title-color        | $font-gray-3                 | -    |
| --cy-cell-group-title-font-size    | 28rpx                        | -    |
| --cy-cell-group-title-line-height  | 90rpx                        | -    |
| --cy-cell-group-title-padding-left | 32rpx                        | -    |
| --cy-cell-bg-color                 | $bg-color-container          | -    |
| --cy-cell-border-color             | $component-stroke            | -    |
| --cy-cell-border-width             | 1px                          | -    |
| --cy-cell-border-left-space        | $cell-horizontal-padding     | -    |
| --cy-cell-border-right-space       | 0                            | -    |
| --cy-cell-description-color        | $font-gray-2                 | -    |
| --cy-cell-description-font-size    | $font-size-base              | -    |
| --cy-cell-description-line-height  | 44rpx                        | -    |
| --cy-cell-height                   | auto                         | -    |
| --cy-cell-horizontal-padding       | 32rpx                        | -    |
| --cy-cell-hover-color              | $bg-color-secondarycontainer | -    |
| --cy-cell-image-height             | 96rpx                        | -    |
| --cy-cell-image-width              | 96rpx                        | -    |
| --cy-cell-left-icon-color          | $brand-color                 | -    |
| --cy-cell-left-icon-font-size      | 48rpx                        | -    |
| --cy-cell-line-height              | 48rpx                        | -    |
| --cy-cell-note-color               | $font-gray-3                 | -    |
| --cy-cell-note-font-size           | $font-size-m                 | -    |
| --cy-cell-required-color           | $error-color-6               | -    |
| --cy-cell-required-font-size       | $font-size-m                 | -    |
| --cy-cell-right-icon-color         | $font-gray-3                 | -    |
| --cy-cell-right-icon-font-size     | 48rpx                        | -    |
| --cy-cell-title-color              | $font-gray-1                 | -    |
| --cy-cell-title-font-size          | $font-size-m                 | -    |
| --cy-cell-vertical-padding         | 32rpx                        | -    |