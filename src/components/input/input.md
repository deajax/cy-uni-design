## 代码演示

#### 基础输入框

```vue
<view class="example">
  <cy-input label="标签文字" placeholder="请输入文字"></cy-input>
  <cy-input label="标签文字" placeholder="请输入文字(选填)" />
  <cy-input placeholder="请输入文字" />
  <cy-input label="标签文字" placeholder="请输入文字" tips="辅助说明" />
</view>
```

#### 带字数限制输入框

```vue
<cy-input label="标签文字" placeholder="请输入文字" tips="最大输入10个字符" :maxlength="10" />
<cy-input label="标签文字" placeholder="请输入文字" tips="最大输入10个字符，汉字算两个" :maxcharacter="10" />
```

#### 带操作输入框

```vue
<view class="example">
  <cy-input
            label="标签文字"
            placeholder="请输入文字"
            :suffixIcon="{ name: 'error-warning-fill', ariaLabel: '提示' }" />
  <cy-input label="标签文字" placeholder="请输入手机号码">
    <cy-button slot="suffix" theme="primary" size="extra-small"> 操作按钮 </cy-button>
  </cy-input>
  <cy-input label="标签文字" placeholder="请输入文字" :suffixIcon="{ name: 'user-line', ariaLabel: '通讯录' }" />
</view>
```

#### 带图标输入框

```vue
<cy-input prefixIcon="apps-line" label="标签文字" placeholder="请输入文字" />
<cy-input prefixIcon="apps-line" placeholder="请输入文字" />
```

#### 特定类型输入框

```vue
<view class="example">
  <cy-input label="输入密码" type="password" :value="textPassword" clearable />
  <cy-input placeholder="输入验证码" label="验证码">
    <view slot="suffix" class="suffix">
      <cy-divider layout="vertical" />
      <image
             class="image"
             src="https://wwcdn.weixin.qq.com/node/wework/images/202010241547.ac6876be9c.png"
             mode="heightFix"
             aria-role="img"
             aria-label="验证码" />
    </view>
  </cy-input>
  <cy-input
            label="手机号"
            placeholder="输入手机号码"
            :value="phoneNumber"
            type="number"
            :tips="phoneError ? '手机号输入不正确' : ''">
    <view slot="suffix" style="display: flex; align-items: center">
      <cy-divider layout="vertical" />
      <view class="verify" aria-role="button"> 发送验证码 </view>
    </view>
  </cy-input>
  <cy-input
            label="价格"
            placeholder="0.00"
            suffix="元"
            align="right"
            type="number"
            :tips="priceError ? '请输入正确的价格' : ''"
            custom-class-tips="tips" />

  <cy-input label="数量" placeholder="填写个数" suffix="个" align="right" type="number" />
</view>

```

```js
export default {
	data() {
		return {
			value: '',
			textPassword: '123456',
			phoneError: false,
			phoneNumber: '17600600600',
			priceError: false,
			style: 'border: 2rpx solid #f3f3f3; border-radius: 12rpx;',
		}
	}
} 
```

```scss
.suffix {
	display: flex;
	align-items: center;
}

.tips {
	text-align: right !important;
}

.verify {
	color: var(--cy-brand-color, #0052D9);
	font-size: 32rpx;
}
```

#### 输入框状态

```vue
<cy-input label="标签文字" placeholder="请输入文字" value="已输入文字" status="error" tips="辅助说明" />
<cy-input label="标签文字" value="不可编辑文字" disabled />
```

#### 信息超长状态

```vue
<cy-input label="标签超长时最多十个字" placeholder="请输入文字" />
```

#### 内容位置

```vue
<cy-input label="左对齐" placeholder="请输入文字" />
<cy-input label="居中" placeholder="请输入文字" align="center" />
<cy-input label="右对齐" placeholder="请输入文字" align="right" />
```

#### 竖排样式

```vue
<cy-input
          label="标签文字"
          layout="vertical"
          placeholder="请输入文字"
          :suffixIcon="{ name: 'error-warning-fill', ariaLabel: '提示' }"></cy-input>
```

#### 标签外置样式

```vue
<view class="input-example">
  <view class="input-example__label">标签文字</view>
  <cy-input
            placeholder="请输入文字"
            borderless
            :suffixIcon="{ name: 'error-circle-filled', ariaLabel: '提示' }"
            :style="style" />
</view>
```

```scss
.input-example {
	--cy-input-vertical-padding: 24rpx;

	background-color: #fff;
	padding: 32rpx;
}

.input-example__label {
	color: var(--cy-text-color-primary);
	font-size: 28rpx;
	line-height: 40rpx;
	margin: 0 8rpx 16rpx;
}
```



## API

### 声明

| 名称              | 类型                   | 默认值            | 说明                                                         | 必传                                                         |
| :---------------- | :--------------------- | :---------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| align             | String                 | left              | 文本内容位置，居左/居中/居右。可选项：left/center/right      | N                                                            |
| layout            | String                 | horizontal        | 标题输入框布局方式。可选项：vertical/horizontal              | N                                                            |
| borderless        | Boolean                | false             | 是否开启无边框模式                                           | N                                                            |
| clearable         | Boolean / Object       | false             | 是否可清空，默认不启动。值为 `true` 表示使用默认清除空按钮，值为 `Object` 表示透传至 `icon` | N                                                            |
| disabled          | Boolean                | false             | 是否禁用输入框                                               | N                                                            |
| label             | String / Slot          | -                 | 左侧文本                                                     | N                                                            |
| maxcharacter      | Number                 | -                 | 用户最多可以输入的字符个数，一个中文汉字表示两个字符长度。`maxcharacter` 和 `maxlength` 二选一使用 | N                                                            |
| maxlength         | Number                 | -1                | 用户最多可以输入的文本长度，一个中文等于一个计数长度。默认为 -1，不限制输入长度。`maxcharacter` 和 `maxlength` 二选一使用 | N                                                            |
| placeholder       | String                 | undefined         | 占位符                                                       | N                                                            |
| prefix-icon       | String / Object / Slot | -                 | 组件前置图标。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon`。 | N                                                            |
| size              | String                 | medium            | 输入框尺寸。可选项：small/medium                             | N                                                            |
| status            | String                 | -                 | 输入框状态。可选项：success/warning/error                    | N                                                            |
| suffix            | String / Slot          | -                 | 后置图标前的后置内容                                         | N                                                            |
| suffix-icon       | String / Object / Slot | -                 | 后置文本内容。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon`。 | N                                                            |
| tips              | String / Slot          | -                 | 输入框下方提示文本，会根据不同的 `status` 呈现不同的样式     | N                                                            |
| type              | String                 | text              | 输入框类型。可选项：text/number/idcard/digit/safe-password/password/nickname | N                                                            |
| value             | String / Number        | -                 | 输入框的值。                                                 | number`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/tree/develop/src/input/type.ts) |
| placeholder-style | String                 | -                 | 必需。指定 placeholder 的样式                                | Y                                                            |
| placeholder-class | String                 | input-placeholder | 指定 placeholder 的样式类                                    | N                                                            |
| cursor-spacing    | Number                 | 0                 | 指定光标与键盘的距离，取 input 距离底部的距离和 cursor-spacing 指定的距离的最小值作为光标与键盘的距离 | N                                                            |
| focus             | Boolean                | false             | 获取焦点                                                     | N                                                            |
| confirm-type      | String                 | done              | 设置键盘右下角按钮的文字，仅在type='text'时生效。 具体释义： `send` 右下角按钮为“发送”； `search` 右下角按钮为“搜索”； `next` 右下角按钮为“下一个”； `go` 右下角按钮为“前往”； `done` 右下角按钮为“完成”。 [小程序官方文档](https://developers.weixin.qq.com/miniprogram/dev/component/input.html)。可选项：send/search/next/go/done | N                                                            |
| always-embed      | Boolean                | false             | 强制 input 处于同层状态，默认 focus 时 input 会切到非同层状态 (仅在 iOS 下生效) | N                                                            |
| confirm-hold      | Boolean                | false             | 点击键盘右下角按钮时是否保持键盘不收起                       | N                                                            |
| cursor            | Number                 | -                 | 必需。指定 focus 时的光标位置                                | Y                                                            |
| selection-start   | Number                 | -1                | 光标起始位置，自动聚集时有效，需与 selection-end 搭配使用    | N                                                            |
| selection-end     | Number                 | -1                | 光标结束位置，自动聚集时有效，需与 selection-start 搭配使用  | N                                                            |
| adjust-position   | Boolean                | true              | 键盘弹起时，是否自动上推页面                                 | N                                                            |
| hold-keyboard     | Boolean                | false             | focus时，点击页面的时候不收起键盘                            | N                                                            |

### 插槽

| 名称        | 描述                 |
| ----------- | -------------------- |
| prefix-icon | 前置图标             |
| label       | 左侧文本             |
| input       | 自定义输入框         |
| suffix      | 后置图标前的后置内容 |
| suffix-icon | 后置文本内容         |
| tips        | 提示文本下方         |

### 事件

| 名称                 | 参数                                                   | 描述                                                   |
| :------------------- | :----------------------------------------------------- | :----------------------------------------------------- |
| blur                 | `(value: InputValue)`                                  | 失去焦点时触发                                         |
| change               | `(value: InputValue, cursor: number, keyCode: number)` | 输入框值发生变化时触发；cursor 为光标位置；            |
| clear                | -                                                      | 清空按钮点击时触发                                     |
| enter                | `(value: InputValue)`                                  | 回车键按下时触发                                       |
| focus                | `(value: InputValue)`                                  | 获得焦点时触发                                         |
| keyboardheightchange | `(height: number, duration: number)`                   | 键盘高度发生变化的时候触发此事件                       |
| nicknamereview       | `(pass: boolean, timeout: boolean)`                    | 用户昵称审核完毕后触发，仅在 type 为 "nickname" 时有效 |

### 外部样式类

| 类名                    | 说明 |
| ----------------------- | ---- |
| custom-class            |      |
| custom-class-prefix     |      |
| custom-class-prefixIcon |      |
| custom-class-label      |      |
| custom-class-content    |      |
| custom-class-input      |      |
| custom-class-suffix     |      |
| custom-class-suffixIcon |      |
| custom-class-tips       |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |