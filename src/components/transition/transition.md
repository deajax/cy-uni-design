## 代码演示

#### 基础用法

```vue
<cy-transition v-model="show" name="fade">
	<view></view>
</cy-transition>
```



## API

### 声明

| 名称            | 类型         | 默认值 | 说明                                                         | 必传 |
| --------------- | ------------ | ------ | ------------------------------------------------------------ | ---- |
| value           | Boolean      | false  | 是否显示                                                     | Y    |
| name            | Array/String | -      | 动画类型，支持fade/slide-top/slide-bottom/slide-right/slide-left/zoom | Y    |
| duration        | Number       | 240    | 动画持续时间                                                 | N    |
| custom-style    | Object       |        | 自定义样式                                                   | N    |
| destroy-on-hide | Boolean      | false  | 是否使用v-if 替代v-show                                      | N    |

### 插槽

| 名称    | 描述                   |
| ------- | ---------------------- |
| default | 默认插槽，用于放置内容 |

### 外部样式类

| 类名         | 说明 |
| ------------ | ---- |
| custom-class |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |