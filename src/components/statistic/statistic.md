## 代码演示

#### 基本用法

```vue
<cy-statistic title="Active Users" :value="112893" />
```

#### 前缀和后缀

```vue
<cy-statistic title="Active Users" :value="112893">
	<view slot="prefix">prefix</view>
</cy-statistic>

<cy-statistic title="Active Users" :value="112893">
	<view slot="suffix">suffix</view>
</cy-statistic>
```



## API

### 声明

| 名称   | 类型            | 默认值 | 说明           | 必传 |
| :----- | :-------------- | :----- | :------------- | :--- |
| title  | String / Slot   |        | 数值的标题     | N    |
| value  | String / number |        | 数值内容       | N    |
| prefix | String          |        | 设置数值的前缀 | N    |
| suffix | String          |        | 设置数值的后缀 | N    |

### 插槽

| 名称    | 描述           |
| ------- | -------------- |
| default | 内容区域       |
| title   | 标题区域后方   |
| value   | 数值内容区域   |
| prefix  | 数值的前缀区域 |
| suffix  | 数值的后缀区域 |

### 事件

| 名称 | 参数 | 描述 |
| ---- | ---- | ---- |
|      |      |      |

### 外部样式类

| 类名                 | 说明 |
| -------------------- | ---- |
| custom-class         |      |
| custom-class-title   |      |
| custom-class-content |      |
| custom-class-prefix  |      |
| custom-class-value   |      |
| custom-class-suffix  |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                         | 默认值                                               | 描述 |
| ---------------------------- | ---------------------------------------------------- | ---- |
| $statistic-title-margin      | var(--cy-statistic-title-margin, 8rpx)               |      |
| $statistic-title-color       | var(--cy-statistic-title-color, $font-gray-3)        |      |
| $statistic-title-font-size   | var(--cy-statistic-title-font-size, $font-size-base) |      |
| $statistic-content-color     | var(--cy-statistic-content-color, $font-gray-1)      |      |
| $statistic-content-font-size | var(--cy-statistic-content-font-size, 48rpx)         |      |