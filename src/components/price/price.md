## 代码演示

#### 不同主题

```vue
<cy-price v-model="price" />

<cy-price v-model="price" theme="primary" />

<cy-price v-model="price" theme="warning" />

<cy-price v-model="price" theme="danger" />

<cy-price v-model="price" theme="success" />
```

#### 不同尺寸

```vue
<cy-price v-model="price" size="small" />

<cy-price v-model="price" size="medium" />

<cy-price v-model="price" size="large" />

<cy-price v-model="price" size="extra-large" />
```

```js
export default {
	data() {
		return {
			price: '39.98'
		}
	}
}
```



## API

### 声明

| 名称  | 类型            | 默认值  | 说明     | 必传 |
| ----- | --------------- | ------- | -------- | ---- |
| value | String / Number | -       | 价格数值 | Y    |
| theme | String          | default | 主题     | N    |
| size  | String          | medium  | 尺寸     | N    |

### 插槽

| 名称        | 说明         |
| ----------- | ------------ |
| default     | 内容区域     |
| prefix-icon | 前缀图标区域 |
| suffix-icon | 后缀图标区域 |

### 外部样式类

| 类名                     | 说明 |
| ------------------------ | ---- |
| custom-class             |      |
| custom-class-content     |      |
| custom-class-prefix-icon |      |
| custom-class-suffix-icon |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |