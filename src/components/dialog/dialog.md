## 代码演示

#### 基础对话框

```vue
<button @click="openDialog">打开弹窗</button>

<!-- 或者
<button @click="$refs.hintPopup.open()">打开弹窗</button>
<button @click="$refs.hintPopup.close()">关闭弹窗</button>
-->

<cy-dialog
  ref="popdialog"
  :closeBtn="closeBtn"
  :closeOnOverlayClick="closeOnOverlayClick"
  :confirm-btn="{ content: '知道了', variant: 'base' }"
  :cancelBtn="cancelBtn"
  title="对话框标题"
  content="告知当前状态、信息和解决方法，等内容。描述文案尽可能控制在三行内"
  @confirm="handleConfirm"
  @cancel="handleCancel"
  @close="handleClose"
/>
```

```js
export default {
data() {
		return {
			closeBtn: false,
			closeOnOverlayClick: false,
		}
	},
  methods: {
    openDialog() {
      this.$refs.popdialog.open();
    },
    handleConfirm(event) {
      console.log('确认按钮点击', event);
    },
    handleCancel(event) {
      console.log('取消按钮点击', event);
    },
    handleClose() {
      this.$refs.popdialog.close()
    }
  }
}
```

#### 垂直基础按钮

```vue
<button @click="openDialog">打开弹窗</button>

<!-- 或者
<button @click="$refs.hintPopup.open()">打开弹窗</button>
<button @click="$refs.hintPopup.close()">关闭弹窗</button>
-->

<cy-dialog
  ref="popdialog"
  button-layout="vertical"
  :closeBtn="closeBtn"
  :closeOnOverlayClick="closeOnOverlayClick"
  :confirm-btn="{ content: '知道了', variant: 'base' }"
  :cancelBtn="cancelBtn"
  title="对话框标题"
  content="告知当前状态、信息和解决方法，等内容。描述文案尽可能控制在三行内"
  @confirm="handleConfirm"
  @cancel="handleCancel"
  @close="handleClose"
/>
```

```js
export default {
data() {
		return {
			closeBtn: false,
			closeOnOverlayClick: false,
		}
	},
  methods: {
    openDialog() {
      this.$refs.popdialog.open();
    },
    handleConfirm(event) {
      console.log('确认按钮点击', event);
    },
    handleCancel(event) {
      console.log('取消按钮点击', event);
    },
    handleClose() {
      this.$refs.popdialog.close()
    }
  }
}
```



## API

### 声明

| 属性名              | 类型          | 默认值         | 描述                                                         |      |
| :------------------ | :------------ | :------------- | :----------------------------------------------------------- | :--- |
| buttonLayout        | String        | `'horizontal'` | 多按钮排列方式，可选值为 `'horizontal'` 或 `'vertical'`。    |      |
| cancelBtn           | Object/String | `null`         | 取消按钮配置，可为 `null`（不显示）、字符串（按钮文本）或对象（按钮属性）。 |      |
| closeBtn            | Boolean       | `false`        | 是否展示关闭按钮，可为 `true`（显示默认关闭按钮）、`false`（不显示）或对象（图标属性）。 |      |
| closeOnOverlayClick | Boolean       | `false`        | 点击蒙层时是否触发关闭事件。                                 |      |
| confirmBtn          | Object/String | `null`         | 确认按钮配置，可为 `null`（不显示）、字符串（按钮文本）或对象（按钮属性）。 |      |
| content             | String        | `''`           | 对话框内容。                                                 |      |
| title               | String        | `''`           | 对话框标题。                                                 |      |
| zIndex              | Number        | `11500`        | 对话框层级，Web 侧样式默认为 `2500`，移动端样式默认 `2500`，小程序样式默认为 `11500`。 |      |

### 插槽

| 名称           | 描述                 |
| -------------- | -------------------- |
| top            | 头部内容，内容上方   |
| middle/default | 中间内容，脚部上方   |
| title          | 标题下方             |
| content        | 内容下方             |
| actions        | 脚部内部，操作栏上方 |
| confirm-btn    | 确认按钮下方         |
| cancel-btn     | 取消按钮下方         |

### 事件

| 名称     | 参数    | 描述                                                         |
| -------- | ------- | ------------------------------------------------------------ |
| @close   | -       | 关闭事件，点击 取消按钮 或 点击蒙层 时触发。                 |
| @cancel  | `event` | 如果“取消”按钮存在，则点击“取消”按钮时触发，同时触发关闭事件 |
| @confirm | `event` | 如果“确认”按钮存在，则点击“确认”按钮时触发                   |

### 方法

| 方法名  | 参数 | 描述         |
| :------ | :--- | :----------- |
| `open`  | 无   | 打开对话框。 |
| `close` | 无   | 关闭对话框。 |

### 外部样式类

| 类名                 | 说明         |
| -------------------- | ------------ |
| custom-class         | 根节点样式类 |
| custom-class-content | 内容样式类   |
| custom-class-confirm | 确认样式类   |
| custom-class-cancel  | 取消样式类   |
| custom-class-action  | 操作样式类   |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                            | 默认值       | 描述 |
| :------------------------------ | :----------- | :--- |
| --cy-dialog-body-max-height     | 912rpx       | -    |
| --cy-dialog-close-color         | $font-gray-3 | -    |
| --cy-dialog-content-color       | $font-gray-2 | -    |
| --cy-dialog-content-font-size   | 32rpx        | -    |
| --cy-dialog-content-line-height | 48rpx        | -    |
| --cy-dialog-title-color         | $font-gray-1 | -    |
| --cy-dialog-title-font-size     | 36rpx        | -    |
| --cy-dialog-title-line-height   | 52rpx        | -    |
| --cy-dialog-width               | 622rpx       | -    |