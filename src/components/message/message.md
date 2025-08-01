## 代码演示

#### 纯文字的通知

```vue
<cy-message content='这是一条普通通知信息' />
```

#### 带图标的通知

```vue
<cy-message icon="information-fill" content='这是一条普通通知信息' />
```

#### 带关闭的通知

```vue
<cy-message icon="information-fill" content='这是一条普通通知信息' :link="{ content: '按钮' }" closeBtn />
```

#### 组件状态

```vue
<cy-message theme="info" content='这是一条普通通知信息' closeBtn />

<cy-message theme="success" content='这是一条成功的提示消息' closeBtn />

<cy-message theme="warning" content='这是一条需要用户关注到的警示通知' closeBtn />

<cy-message theme="error" content='这是一条错误提示通知' closeBtn />
```



## API

### 声明

| 名称     | 类型          | 默认值 | 说明                                                         | 必传 |
| -------- | ------------- | ------ | ------------------------------------------------------------ | ---- |
| align    | String        | 'left' | 文本对齐方式                                                 | N    |
| closeBtn | null          | false  | 闭按钮，可以自定义。值为 true 显示默认关闭按钮，值为 false 不显示关闭按钮。值类型为 string 则直接显示值，如：“关闭”。也可以完全自定义按钮 | N    |
| content  | String        | -      | 用于自定义消息弹出内容                                       | N    |
| icon     | String/Object | -      | 消息提醒前面的图标。也可以完全自定义图标节点                 | N    |
| theme    | String        | 'info' | 消息组件风格                                                 | N    |
| link     | null          | -      | 链接名称。值为字符串表示链接名称，值为 `Object` 类型，表示透传至 `Link`。 | N    |

### 插槽

| 名称      | 描述             |
| --------- | ---------------- |
| default   | 内容区域默认插槽 |
| icon      | 图标区域插槽     |
| content   | 内容区域插槽     |
| link      | 右侧区域插槽     |
| close-btn | 关闭按钮插槽     |

### 外部样式类

| 类名                   | 说明 |
| ---------------------- | ---- |
| custom-class           |      |
| custom-class-content   |      |
| custom-class-link      |      |
| custom-class-close-btn |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |