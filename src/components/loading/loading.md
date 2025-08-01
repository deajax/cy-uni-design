## 代码演示

#### 纯图标

```vue
<cy-loading></cy-loading>
```

#### 图标加文字横向

```vue
<cy-loading text="加载中..."></cy-loading>
```

#### 图标加文字竖向

```vue
<cy-loading text="加载中" layout="vertical"></cy-loading>
```

#### 纯文字

```vue
<cy-loading text="加载中..." :indicator="false"></cy-loading>
```

#### 组件颜色

```vue
<cy-loading text="加载中..." color="blue"></cy-loading>

<cy-loading text="加载中..." color="red"></cy-loading>

<cy-loading text="加载中..." color="gray"></cy-loading>
```

#### 配合Empty组件制作页面加载效果

```vue
<cy-empty description="数据加载中">
  <template #icon>
		<cy-loading />
  </template>
</cy-empty>
```

## API

### 声明

| 名称      | 类型             | 默认值     | 说明                                                         | 必传 |
| --------- | ---------------- | ---------- | ------------------------------------------------------------ | ---- |
| text      | String           | -          | 加载提示文案                                                 | N    |
| color     | String           | -          | 加载组件颜色                                                 | N    |
| layout    | String           | horizontal | 对齐方式。可选项：horizontal/vertical                        | N    |
| indicator | Boolean          | true       | 加载指示符，值为 true 显示默认指示符，值为 false 则不显示，也可以自定义指示符 | N    |
| duration  | String \| Number | 800        | 加载动画执行完成一次的时间，单位：毫秒                       | N    |

### 插槽

| 名称      | 描述               |
| --------- | ------------------ |
| default   | 默认插槽，文字下方 |
| indicator | 图标插槽           |
| text      | 文字插槽           |

### 外部样式类

| 类名                   | 说明 |
| ---------------------- | ---- |
| custom-class           |      |
| custom-class-indicator |      |
| custom-class-circular  |      |
| custom-class-text      |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |