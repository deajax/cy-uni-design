## 代码演示

#### 基础多行文本框

```vue
<cy-textarea placeholder="请输入文字" disable-default-padding />
```

#### 带标题多行文本框

```vue
<cy-textarea label="标签文字" placeholder="请输入文字" disable-default-padding />
```

#### 自动增高多行文本框

```vue
<cy-textarea
						 label="标签文字"
						 placeholder="请输入文字"
						 disable-default-padding
						 autosize
						 @line-change="onLineChange" />
```

#### 设置最大字符个数

```vue
<cy-textarea
						 label="标签文字"
						 placeholder="设置最大字符个数"
						 maxlength="200"
						 disable-default-padding
						 indicator />
```

#### 禁用多行文本框

```vue
<cy-textarea
						 label="标签文字"
						 placeholder="请输入文字"
						 value="不可编辑文字"
						 disable-default-padding
						 disabled />
```

#### 标签外置输入框

```vue
<cy-textarea
             custom-class="external-class"
             placeholder="请输入文字"
             bordered
             maxlength="100"
             disable-default-padding
             indicator
             :custom-style="style" />
```

```js
export default {
	components: {},
	data() {
		return {
			style: 'height: 248rpx',
		}
	},
}
```





## API

### 声明

| 名称              | 类型                     | 默认值     | 描述                                                         | 必传 |
| :---------------- | :----------------------- | :--------- | :----------------------------------------------------------- | :--- |
| allowInputOverMax | Boolean                  | false      | 超出maxlength或maxcharacter之后是否还允许输入                | N    |
| autofocus         | Boolean                  | false      | 自动聚焦，拉起键盘                                           | N    |
| autosize          | Boolean                  | false      | 是否自动增高，值为 autosize 时，style.height 不生效          | N    |
| bordered          | Boolean                  | false      | 是否显示外边框                                               | N    |
| disabled          | Boolean                  | undefined  | 是否禁用文本框                                               | N    |
| indicator         | Boolean                  | false      | 显示文本计数器，如 0/140。当 `maxlength < 0 && maxcharacter < 0` 成立时， indicator无效 | N    |
| label             | String / Slot / Function | -          | 左侧文本。https://github.com/Tencent/tdesign-mobile-vue/blob/develop/src/common.ts) | N    |
| layout            | String                   | horizontal | 标题输入框布局方式。可选项：vertical/horizontal              | N    |
| maxcharacter      | Number                   | -          | 用户最多可以输入的字符个数，一个中文汉字表示两个字符长度     | N    |
| maxlength         | Number                   | -          | 用户最多可以输入的字符个数                                   | N    |
| name              | String                   | -          | 名称，HTML 元素原生属性                                      | N    |
| placeholder       | String                   | undefined  | 占位符                                                       | N    |
| readonly          | Boolean                  | false      | 只读状态                                                     | N    |
| value             | String / Number          | -          | 文本框值。支持语法糖 `v-model` 或 `v-model:value`。          | N    |
| defaultValue      | String / Number          | -          | 文本框值。非受控属性。https://github.com/Tencent/tdesign-mobile-vue/tree/develop/src/textarea/type.ts) | N    |
| onBlur            | Function                 |            | TS 类型：`(value: TextareaValue, context: { e: FocusEvent }) => void` 失去焦点时触发 | N    |
| onChange          | Function                 |            | TS 类型：`(value: TextareaValue, context?: { e?: InputEvent }) => void` 输入内容变化时触发 | N    |
| onFocus           | Function                 |            | TS 类型：`(value: TextareaValue, context : { e: FocusEvent }) => void` 获得焦点时触发 | N    |

### 事件

| 名称   | 参数                                                   | 描述               |
| :----- | :----------------------------------------------------- | :----------------- |
| blur   | `(value: TextareaValue, context: { e: FocusEvent })`   | 失去焦点时触发     |
| change | `(value: TextareaValue, context?: { e?: InputEvent })` | 输入内容变化时触发 |
| focus  | `(value: TextareaValue, context : { e: FocusEvent })`  | 获得焦点时触发     |

### 插槽

| 名称    | 描述                     |
| ------- | ------------------------ |
| default | 默认插槽，用于自定义样式 |
| label   | 左侧文本插槽             |

### 外部样式类

| 类名                 | 说明 |
| -------------------- | ---- |
| custom-class         |      |
| custom-class-label   |      |
| custom-class-wrapper |      |
| custom-class-indicator |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |