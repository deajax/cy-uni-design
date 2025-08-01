## 代码演示

#### 基础分割符

```
<cy-divider />
```

#### 带文字水平分割线

```
<cy-divider content="文字信息" align="left" />
<cy-divider content="文字信息" />
<cy-divider content="文字信息" align="right" />
```

#### 垂直分割线

```
<view class="flex">
  <text>文字信息</text>
  <cy-divider layout="vertical" />
  <text>文字信息</text>
  <cy-divider layout="vertical" />
  <text>文字信息</text>
</view>
```

#### 虚线样式

```
<cy-divider dashed />
<cy-divider dashed content="文字信息" align="left" />
<cy-divider dashed content="文字信息" />
<cy-divider dashed content="文字信息" align="right" />
```



## API

### 声明

| 名称    | 类型          | 默认值     | 说明                                                      | 必传 |
| :------ | :------------ | :--------- | :-------------------------------------------------------- | :--- |
| align   | String        | center     | 文本位置（仅在水平分割线有效）。可选项：left/right/center | N    |
| content | String / Slot | -          | 子元素                                                    | N    |
| dashed  | Boolean       | false      | 是否虚线（仅在水平分割线有效）                            | N    |
| layout  | String        | horizontal | 分隔线类型有两种：水平和垂直。可选项：horizontal/vertical | N    |

### 插槽

| 类名    | 说明 |
| :------ | :--- |
| content | 内容 |

### 外部样式类

| 类名                 | 说明         |
| :------------------- | :----------- |
| custom-class         | 根节点样式类 |
| custom-class-content | 内容样式类   |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                             | 默认值              | 描述 |
| :------------------------------- | :------------------ | :--- |
| --cy-divider-color               | $bg-color-component | -    |
| --cy-divider-content-color       | $font-gray-3        | -    |
| --cy-divider-content-font-size   | 24rpx               | -    |
| --cy-divider-content-line-height | 40rpx               | -    |
| --cy-divider-content-line-style  | solid               | -    |