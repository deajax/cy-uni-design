## 代码演示

### 组件类型

##### 基础标签

```vue
<cy-tag variant="light">标签文字</cy-tag>
<cy-tag variant="outline">标签文字</cy-tag>
```

##### 圆弧标签

```vue
<cy-tag variant="light" shape="round">标签文字</cy-tag>
<cy-tag variant="outline" shape="round">标签文字</cy-tag>
<cy-tag variant="outline" shape="mark">标签文字</cy-tag>
```

##### 带图标的标签

```vue
<cy-tag variant="light" icon="information-line">标签文字</cy-tag>
<cy-tag variant="outline" icon="information-line">标签文字</cy-tag>
<cy-tag variant="outline" :icon="{ name: 'information-line', color: 'red', size: '24' }">标签文字</cy-tag>
```

##### 超长省略文本标签

```vue
<cy-tag max-width="130" variant="light">超长省略文本标签超长省略文本标签</cy-tag>
```

##### 可关闭的标签

```vue
<cy-tag @close="handleClose0" closable variant="light">文字标签</cy-tag>
<cy-tag @close="handleClose1" closable variant="outline">文字标签</cy-tag>
```

### 组件状态

```vue
<view class="example">
  <cy-tag variant="light">默认</cy-tag>
  <cy-tag variant="light" theme="primary">主要</cy-tag>
  <cy-tag variant="light" theme="warning">警告</cy-tag>
  <cy-tag variant="light" theme="danger">危险</cy-tag>
  <cy-tag variant="light" theme="success">成功</cy-tag>
</view>

<view class="example">
  <cy-tag theme="default">默认</cy-tag>
  <cy-tag theme="primary">主要</cy-tag>
  <cy-tag theme="warning">警告</cy-tag>
  <cy-tag theme="danger">危险</cy-tag>
  <cy-tag theme="success">成功</cy-tag>
</view>

<view class="example">
  <cy-tag variant="outline">默认</cy-tag>
  <cy-tag variant="outline" theme="primary">主要</cy-tag>
  <cy-tag variant="outline" theme="warning">警告</cy-tag>
  <cy-tag variant="outline" theme="danger">危险</cy-tag>
  <cy-tag variant="outline" theme="success">成功</cy-tag>
</view>

<view class="example">
  <cy-tag variant="light-outline">默认</cy-tag>
  <cy-tag variant="light-outline" theme="primary">主要</cy-tag>
  <cy-tag variant="light-outline" theme="warning">警告</cy-tag>
  <cy-tag variant="light-outline" theme="danger">危险</cy-tag>
  <cy-tag variant="light-outline" theme="success">成功</cy-tag>
</view>
```

### 组件尺寸

```vue
<cy-tag size="extra-large" variant="light" closable>加大尺寸</cy-tag>
<cy-tag size="large" variant="light" closable>大尺寸</cy-tag>
<cy-tag size="medium" variant="light" closable>中尺寸</cy-tag>
<cy-tag size="small" variant="light" closable>小尺寸</cy-tag>
```



## API

### 声明

| 名称      | 类型                   | 默认值  | 描述                                                         | 必传 |
| :-------- | :--------------------- | :------ | :----------------------------------------------------------- | :--- |
| closable  | Boolean / Object       | false   | 标签是否可关闭                                               | N    |
| disabled  | Boolean                | false   | 标签禁用态，失效标签不能触发事件。默认风格（theme=default）才有禁用态 | N    |
| icon      | String / Object / Slot | -       | 标签中的图标，可自定义图标呈现。[通用类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/src/common/common.ts) | N    |
| max-width | String / Number        | -       | 标签最大宽度，宽度超出后会出现省略号。示例：'50px' / 80 (skyline暂不支持该属性) | N    |
| shape     | String                 | square  | 标签类型，有三种：方形、圆角方形、标记型。可选项：square/round/mark | N    |
| size      | String                 | medium  | 标签尺寸。可选项：small/medium/large/extra-large             | N    |
| theme     | String                 | default | 组件风格，用于描述组件不同的应用场景。可选项：default/primary/warning/danger/success | N    |
| variant   | String                 | dark    | 标签风格变体。可选项：dark/light/outline/light-outline       | N    |

### 事件

| 名称   | 参数 | 描述                                 |
| :----- | :--- | :----------------------------------- |
| @click | -    | 点击时触发                           |
| @close | -    | 如果关闭按钮存在，点击关闭按钮时触发 |

### 外部样式类

| 类名                  | 说明 |
| --------------------- | ---- |
| custom-class          |      |
| custom-class-icon     |      |
| custom-class-text     |      |
| custom-class-closable |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |