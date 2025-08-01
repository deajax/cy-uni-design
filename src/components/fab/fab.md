## 代码演示

#### 基础展示

```vue
<cy-fab :scroll-top="scrollTop">
	solt
</cy-fab>
```

```js
export default {
	data() {
		return {
			scrollTop: 0
		}
	},
	methods: {
		onPageScroll(e) {
			this.scrollTop = e.scrollTop;
		},
	},
}
```

#### 回到顶部

```vue
<cy-fab :scrollTop="scrollTop" backtop />
```



## API

### 声明

| 名称         | 类型    | 默认值                     | 说明                           | 必传 |
| ------------ | ------- | -------------------------- | ------------------------------ | ---- |
| backtop      | Boolean | false                      | 是否开启返回顶部按钮           | N    |
| custom-style | String  | right: 16px; bottom: 32px; | 悬浮按钮的样式，常用于调整位置 | N    |
| scrollTop    | Number  | 0                          | 顶部距离                       | Y    |

### 插槽

| 名称    | 描述       |
| ------- | ---------- |
| default | 自定义内容 |

### 事件

| 名称   | 参数    | 描述                                      |
| ------ | ------- | ----------------------------------------- |
| @toTop | `event` | 返回顶部按钮事件，仅在backtop为true时生效 |

### 外部样式类

| 类名                 | 说明               |
| -------------------- | ------------------ |
| custom-class         | 根节点样式类       |
| custom-class-backtop | 返回顶部按钮样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。



| 名称                   | 默认值       | 描述 |
| ---------------------- | ------------ | ---- |
| --cy-fab-shadow        | $shadow-2    | -    |
| --cy-fab-backtop-color | $brand-color | -    |