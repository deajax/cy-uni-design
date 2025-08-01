## 代码演示

#### 纯文字的公告栏

```vue
<cy-notice-bar content="这是一条普通的通知信息" :prefixIcon="false" />
```

#### 带图标的公告栏

```vue
<cy-notice-bar prefix-icon="information-fill" content="提示文字描述提示文字描述提示文字描述" />

<cy-notice-bar :prefixIcon="false" content="提示文字描述提示文字描述提示文字描述">
  <view slot="prefix-icon">
    <cy-icon name="information-fill"></cy-icon>
  </view>
</cy-notice-bar>
```

#### 带关闭的公告栏

```vue
<cy-notice-bar suffix-icon="close-line" content="这是一条普通的通知信息" />
```

#### 带入口的公告栏

```vue
<cy-notice-bar suffix-icon="arrow-right-s-line">
  <view slot="content" style="display: inline-flex;">
    <text>这是一条普通的通知信息</text>
    <cy-text content="详情" theme="primary" />
  </view>
</cy-notice-bar>
```

#### 组件状态

```vue
<cy-notice-bar prefix-icon="information-fill" content="默认状态公告栏默认状态公告栏" />
<cy-notice-bar prefix-icon="checkbox-circle-fill" theme="success" content="成功状态公告栏成功状态公告栏" />
<cy-notice-bar prefix-icon="information-fill" theme="warning" content="警示状态公告栏警示状态公告栏" />
<cy-notice-bar prefix-icon="information-fill" theme="error" content="错误状态公告栏错误状态公告栏" />
```

#### 可滚动公告栏

```vue
<!-- 跑马灯滚动 -->
<cy-notice-bar prefix-icon="volume-up-line" content="君不见高堂明镜悲白发，朝如青丝暮成雪" theme="error" marquee />

<!-- 行滚动 -->
<cy-notice-bar prefix-icon="volume-up-line" :content="content" direction="vertical" />
```

```js
export default {
	components: {},
	data() {
		return {
			content: ['君不见高堂明镜悲白发', '朝如青丝暮成雪', '人生得意须尽欢', '莫使金樽空对月']
		}
	}
}
```



## API

### 声明

| 名称        | 类型                             | 默认值     | 说明                                                         | 必传 |
| :---------- | :------------------------------- | :--------- | :----------------------------------------------------------- | :--- |
| content     | String / Array / Slot            | -          | 文本内容                                                     | N    |
| direction   | String                           | horizontal | 滚动方向。可选项：horizontal/vertical                        | N    |
| operation   | String / Slot                    | -          | 右侧额外信息                                                 | N    |
| marquee     | Boolean                          | false      | 是否开启跑马灯效果【仅在 direction='horizontal' 有效】。     | N    |
| interval    | Number                           | 2000       | 间隔时间【仅在 direction='vertical' 有效】。                 | N    |
| prefix-icon | String / Boolean / Object / Slot | -          | 前缀图标。值为字符串表示图标名称，值为 `false` 表示不显示前缀图标，值为 `Object` 类型，表示透传至 `icon`，不传表示使用主题图标。 | N    |
| suffix-icon | String / Object / Slot           | -          | 后缀图标。值为字符串表示图标名称。值为 `Object` 类型，表示透传至 `icon`，不传表示不显示后缀图标。 | N    |
| theme       | String                           | info       | 内置主题。可选项：info/success/warning/error                 | N    |
| visible     | Boolean                          | false      | 显示/隐藏                                                    | N    |

### 插槽

| 名称        | 描述         |
| ----------- | ------------ |
| prefix-icon | 前缀图标区域 |
| content     | 内容区域     |
| suffix-icon | 后缀图标区域 |

### 事件

| 名称    | 参数 | 描述         |
| ------- | ---- | ------------ |
| @click  | -    | 点击事件     |
| @suffix | -    | 后缀图标事件 |

### 外部样式类

| 类名                     | 说明 |
| ------------------------ | ---- |
| custom-class             |      |
| custom-class-prefix-icon |      |
| custom-class-wrapper     |      |
| custom-class-content     |      |
| custom-class-item        |      |
| custom-class-operation   |      |
| custom-class-suffix-icon |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |