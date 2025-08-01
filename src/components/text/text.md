## 代码演示

#### 基础文字链接

```
<view class="example">
  <cy-text size="small" theme="primary" content="文本内容" hover />
  <cy-text size="small" content="文本内容" hover />
</view>
```

#### 下划线文字链接

```
<view class="example">
  <cy-text size="small" theme="primary" content="文本内容" underline hover />
  <cy-text size="small" content="文本内容" underline hover />
</view>
```

#### 前置图标文字链接

```
<view class="example">
  <cy-text size="small" theme="primary" content="文本内容" prefixIcon="links-line" hover />
  <cy-text size="small" content="文本内容" prefixIcon="links-line" hover />
</view>
```

#### 后置图标文字链接

```
<view class="example">
  <cy-text size="small" theme="primary" content="文本内容" suffixIcon="share-line" hover />
  <cy-text size="small" content="文本内容" suffixIcon="share-line" hover />
</view>
```

#### 不同主题

```
<view class="example">
  <cy-text size="small" theme="primary" content="文本内容" suffixIcon="share-line" hover />
  <cy-text size="small" content="文本内容" suffixIcon="share-line" hover />
  <cy-text size="small" theme="danger" content="文本内容" suffixIcon="share-line" hover />
  <cy-text size="small" theme="warning" content="文本内容" suffixIcon="share-line" hover />
  <cy-text size="small" theme="success" content="文本内容" suffixIcon="share-line" hover />
</view>
```

#### 禁用状态

```
<view class="example">
  <cy-text
  size="small"
  theme="primary"
  content="文本内容"
  suffixIcon="share-line"
  disabled
  hover />
  <cy-text size="small" content="文本内容" suffixIcon="share-line" disabled />
  <cy-text size="small" theme="danger" content="文本内容" suffixIcon="share-line" disabled />
  <cy-text size="small" theme="warning" content="文本内容" suffixIcon="share-line" disabled />
  <cy-text size="small" theme="success" content="文本内容" suffixIcon="share-line" disabled />
</view>
```

#### 组件尺寸

```
<view class="example">
  <cy-text size="small" theme="primary" content="S号链接" suffixIcon="share-line" hover />
  <cy-text theme="primary" content="M号链接" suffixIcon="share-line" hover />
  <cy-text size="large" theme="primary" content="L号链接" suffixIcon="share-line" hover />
</view>
```



## API

### 声明

| 名称        | 类型                   | 默认值  | 说明                                                         | 必传 |
| :---------- | :--------------------- | :------ | :----------------------------------------------------------- | :--- |
| content     | String / Slot          | -       | 内容                                                         | N    |
| prefix-icon | String / Object / Slot | -       | 前置图标                                                     | N    |
| size        | String                 | medium  | 尺寸。可选项：small/medium/large                             | N    |
| disabled    | Boolean                | false   | 是否为禁用态                                                 | N    |
| hover       | Boolean                | -       | 是否开启点击反馈                                             | N    |
| suffix-icon | String / Object / Slot | -       | 后置图标                                                     | N    |
| theme       | String                 | default | 组件风格，依次为默认色、品牌色、危险色、警告色、成功色。可选项：default/primary/danger/warning/success | N    |
| underline   | Boolean                | -       | 是否显示链接下划线                                           | N    |
| url         | String                 | -       | 当前小程序内的跳转链接                                       | N    |

### 插槽

| 名称        | 描述                     |
| :---------- | :----------------------- |
| default     | 默认插槽（内容插槽后方） |
| prefix-icon | 前置图标                 |
| content     | 内容                     |
| suffix-icon | 后置图标                 |

### 事件

| 名称   | 参数    | 描述                                     |
| :----- | :------ | :--------------------------------------- |
| @click | `event` | 点击按钮，当按钮不为加载或禁用状态时触发 |

### 外部样式类

| 类名                     | 说明           |
| :----------------------- | :------------- |
| custom-class             | 根节点样式类   |
| custom-class-prefix-icon | 前置图标样式类 |
| custom-class-content     | 内容样式类     |
| custom-class-suffix-icon | 后置图标样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                             | 默认值                  | 描述 |
| :------------------------------- | :---------------------- | :--- |
| --cy-link-danger-active-color    | @error-color-active     | -    |
| --cy-link-danger-color           | @error-color            | -    |
| --cy-link-danger-disabled-color  | @error-color-disabled   | -    |
| --cy-link-default-active-color   | @brand-color-active     | -    |
| --cy-link-default-color          | @font-gray-1            | -    |
| --cy-link-default-disabled-color | @text-color-disabled    | -    |
| --cy-link-primary-active-color   | @brand-color-active     | -    |
| --cy-link-primary-color          | @brand-color            | -    |
| --cy-link-primary-disabled-color | @brand-color-disabled   | -    |
| --cy-link-success-active-color   | @success-color-active   | -    |
| --cy-link-success-color          | @success-color          | -    |
| --cy-link-success-disabled-color | @success-color-disabled | -    |
| --cy-link-warning-active-color   | @warning-color-active   | -    |
| --cy-link-warning-color          | @warning-color          | -    |
| --cy-link-warning-disabled-color | @warning-color-disabled | -    |