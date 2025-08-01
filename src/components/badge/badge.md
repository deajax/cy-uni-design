## 代码演示

#### 红点徽标

```
<cy-badge dot class="wrapper" content="消息" />

<cy-badge dot class="wrapper">
	<cy-icon name="notification-4-line" size="48" />
</cy-badge>

<cy-badge dot class="wrapper">
	<cy-button>按钮</cy-button>
</cy-badge>
```

#### 数字徽标

```
<cy-badge count="8" content="消息" class="wrapper" />

<cy-badge count="2" class="wrapper">
	<cy-icon name="notification-4-line" size="48" />
</cy-badge>

<cy-badge count="38" class="wrapper">
	<cy-button>按钮</cy-button>
</cy-badge>
```

#### 大尺寸

```
<cy-badge count="8" content="消息" size="large" />

<cy-badge count="2" size="large">
	<cy-icon name="notification-4-line" size="48" />
</cy-badge>

<cy-badge count="38" size="large">
	<cy-button>按钮</cy-button>
</cy-badge>
```

#### 自定义徽标

```
<cy-badge count="NEW">
	<cy-button icon="notification-4-line" shape="square" size="large" />
</cy-badge>
```

#### 单独使用

```
<cy-cell title="单独使用">
	<cy-badge slot="right-icon" count="13" />
</cy-cell>
```



## API

### 声明

| 名称    | 类型                   | 默认值 | 说明                                                         | 必传 |
| :------ | :--------------------- | :----- | :----------------------------------------------------------- | :--- |
| color   | String                 | -      | 颜色                                                         | N    |
| content | String                 | -      | 徽标内容，示例：`content='自定义内容'`。也可以使用默认插槽定义 | N    |
| count   | String / Number / Slot | 0      | 徽标右上角内容。可以是数字，也可以是文字。如：'new'/3/90。特殊：值为空表示使用插槽渲染。 | N    |
| dot     | Boolean                | false  | 是否为红点                                                   | N    |
| size    | String                 | medium | 尺寸。可选项：medium/large                                   |      |

### 插槽

| 名称    | 描述           |
| ------- | -------------- |
| default | 内容后方       |
| count   | 计数后方       |
| badge   | 自定义徽标内容 |

### 外部样式类

| 类名                 | 说明         |
| -------------------- | ------------ |
| custom-class         | 根节点样式类 |
| custom-class-count   | 计数样式类   |
| custom-class-content | 内容样式类   |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                            | 默认值                | 描述 |
| :------------------------------ | :-------------------- | :--- |
| --cy-badge-basic-height         | 32rpx                 | -    |
| --cy-badge-basic-padding        | 8rpx                  | -    |
| --cy-badge-basic-width          | 32rpx                 | -    |
| --cy-badge-bg-color             | $error-color          | -    |
| --cy-badge-border-radius        | 4rpx                  | -    |
| --cy-badge-bubble-border-radius | 20rpx 20rpx 20rpx 1px | -    |
| --cy-badge-dot-size             | 16rpx                 | -    |
| --cy-badge-font-size            | $font-size-xs         | -    |
| --cy-badge-font-weight          | 600                   | -    |
| --cy-badge-large-font-size      | $font-size-s          | -    |
| --cy-badge-large-height         | 40rpx                 | -    |
| --cy-badge-large-padding        | 10rpx                 | -    |
| --cy-badge-text-color           | $font-white-1         | -    |