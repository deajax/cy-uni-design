## 代码演示

#### 基础按钮

```
<cy-button theme="primary" size="large">填充按钮</cy-button>
<cy-button theme="light" size="large">填充按钮</cy-button>
<cy-button size="large">填充按钮</cy-button>
<cy-button theme="primary" size="large" variant="outline">描边按钮</cy-button>
<cy-button size="large" variant="text">文字按钮</cy-button>
```

#### 图标按钮

```
<cy-button theme="primary" icon="search-line" content="填充按钮" size="large"></cy-button>
<cy-button theme="primary" size="large" loading>加载中</cy-button>
<cy-button theme="primary" icon="search-line" shape="square" size="large"></cy-button>
```

#### 幽灵按钮

```
<cy-button theme="primary" ghost size="large">幽灵按钮</cy-button>
<cy-button theme="danger" ghost size="large">幽灵按钮</cy-button>
<cy-button ghost size="large">幽灵按钮</cy-button>
```

#### 通栏按钮

```
<cy-button theme="primary" size="large" block>填充按钮</cy-button>
```

#### 按钮禁用

```
<cy-button theme="primary" size="large" disabled>填充按钮</cy-button>
<cy-button theme="light" size="large" disabled>填充按钮</cy-button>
<cy-button size="large" disabled>填充按钮</cy-button>
<cy-button theme="primary" size="large" variant="outline" disabled>描边按钮</cy-button>
<cy-button theme="primary" size="large" variant="text" disabled>文字按钮</cy-button>
```

#### 按钮尺寸

```
<cy-button theme="primary" icon="search-line" size="large">按钮48</cy-button>
<cy-button theme="primary" icon="search-line">按钮40</cy-button>
<cy-button theme="primary" icon="search-line" size="small">按钮32</cy-button>
<cy-button theme="primary" icon="search-line" size="extra-small">按钮28</cy-button>
```

#### 按钮形状

```
<cy-button theme="primary" size="large">填充按钮</cy-button>
<cy-button theme="primary" size="large" icon="search-line" shape="square"></cy-button>
<cy-button theme="primary" size="large" shape="round">填充按钮</cy-button>
<cy-button theme="primary" size="large" icon="search-line" shape="circle"></cy-button>

<cy-button theme="primary" size="large" block t-class="external-class">填充按钮</cy-button>
```

#### 按钮主题

```
<view class="example">
  <cy-button size="large">填充按钮</cy-button>
  <cy-button size="large" variant="outline">描边按钮</cy-button>
  <cy-button size="large" variant="text">文字按钮</cy-button>
</view>

<view class="example">
  <cy-button size="large" theme="primary">填充按钮</cy-button>
  <cy-button size="large" theme="primary" variant="outline">描边按钮</cy-button>
  <cy-button size="large" theme="primary" variant="text">文字按钮</cy-button>
</view>

<view class="example">
  <cy-button size="large" theme="danger">填充按钮</cy-button>
  <cy-button size="large" theme="danger" variant="outline">描边按钮</cy-button>
  <cy-button size="large" theme="danger" variant="text">文字按钮</cy-button>
</view>

<view class="example">
  <cy-button size="large" theme="light">填充按钮</cy-button>
  <cy-button size="large" theme="light" variant="outline">描边按钮</cy-button>
  <cy-button size="large" theme="light" variant="text">文字按钮</cy-button>
</view>
```



## API

### 声明

| 名称                       | 类型            | 默认值       | 说明                                                         | 必传 |
| :------------------------- | :-------------- | :----------- | :----------------------------------------------------------- | :--- |
| id                         | String          | -            | 按钮标签id                                                   | N    |
| block                      | Boolean         | false        | 是否为块级元素                                               | N    |
| content                    | String / Slot   | -            | 按钮内容                                                     | N    |
| disabled                   | Boolean         | false        | 禁用状态                                                     | N    |
| ghost                      | Boolean         | false        | 是否为幽灵按钮（镂空按钮）                                   | N    |
| icon                       | String / Object | -            | 图标名称。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon`。 | N    |
| loading                    | Boolean         | false        | 是否显示为加载状态，skyline模式下暂不支持该属性              | N    |
| shape                      | String          | rectangle    | 按钮形状，有 4 种：长方形、正方形、圆角长方形、圆形。可选项：rectangle/square/round/circle | N    |
| size                       | String          | medium       | 组件尺寸。可选项：extra-small/small/medium/large             | N    |
| suffix                     | Slot            | -            | 右侧内容，可用于定义右侧图标                                 | N    |
| theme                      | String          | default      | 组件风格，依次为品牌色、危险色。可选项：default/primary/danger/light | N    |
| type                       | String          | -            | 同小程序的 formType。可选项：submit/reset                    | N    |
| variant                    | String          | base         | 按钮形式，基础、线框、文字。可选项：base/outline/dashed/text | N    |
| open-type                  | String          | -            | 开放能力                                                     | N    |
| hover-class                | String          | ''           | 指定按钮按下去的样式类，按钮不为加载或禁用状态时有效。当 `hover-class="none"` 时，没有点击态效果 | N    |
| hover-stop-propagation     | Boolean         | false        | 指定是否阻止本节点的祖先节点出现点击态                       | N    |
| hover-start-time           | Number          | 20           | 按住后多久出现点击态，单位毫秒                               | N    |
| hover-stay-time            | Number          | 70           | 手指松开后点击态保留时间，单位毫秒                           | N    |
| lang                       | String          | en           | 指定返回用户信息的语言，zh_CN 简体中文，zh_TW 繁体中文，en 英文。 | N    |
| session-from               | String          | -            | 会话来源，open-type="contact"时有效                          | N    |
| send-message-title         | String          | 当前标题     | 会话内消息卡片标题，open-type="contact"时有效                | N    |
| send-message-path          | String          | 当前分享路径 | 会话内消息卡片点击跳转小程序路径，open-type="contact"时有效  | N    |
| send-message-img           | String          | 截图         | 会话内消息卡片图片，open-type="contact"时有效                | N    |
| app-parameter              | String          | -            | 打开 APP 时，向 APP 传递的参数，open-type=launchApp时有效    | N    |
| show-message-card          | Boolean         | false        | 是否显示会话内消息卡片，设置此参数为 true，用户进入客服会话会在右下角显示"可能要发送的小程序"提示，用户点击后可以快速发送小程序消息，open-type="contact"时有效 | N    |
| @getuserinfo               | Eventhandle     | -            | 用户点击该按钮时，会返回获取到的用户信息，回调的 detail 数据与[uni.getUserInfo](https://uniapp.dcloud.net.cn/api/plugins/login.html#getuserinfo)返回的一致，open-type="getUserInfo"时有效 | N    |
| @contact                   | Eventhandle     | -            | 客服消息回调，open-type="contact"时有效                      | N    |
| @getphonenumber            | Eventhandle     | -            | 获取用户手机号回调，open-type=getPhoneNumber时有效           | N    |
| @error                     | Eventhandle     | -            | 当使用开放能力时，发生错误的回调，open-type=launchApp时有效  | N    |
| @opensetting               | Eventhandle     | -            | 在打开授权设置页后回调，open-type=openSetting时有效          | N    |
| @launchapp                 | Eventhandle     | -            | 打开 APP 成功的回调，open-type=launchApp时有效               | N    |
| @chooseavatar              | Eventhandle     | -            | 获取用户头像回调，open-type=chooseAvatar时有效               | N    |
| @agreeprivacyauthorization | Eventhandle     | -            | 用户同意隐私协议事件回调，open-type=agreePrivacyAuthorization时有效 | N    |

### 插槽

| 名称    | 描述       |
| :------ | :--------- |
| default | 在内容后方 |
| content | 在内容前方 |
| suffix  | 后缀       |

### 事件

| 名称   | 参数    | 描述                                     |
| :----- | :------ | :--------------------------------------- |
| @click | `event` | 点击按钮，当按钮不为加载或禁用状态时触发 |

### 外部样式类

| 类名               | 说明         |
| ------------------ | ------------ |
| customClass        | 根节点样式类 |
| customClassIcon    | 图标样式类   |
| customClassContent | 内容样式类   |

### CSS 变量

组件提供了 CSS 变量，具体变量请在「开发者工具 - 元素」内查看

| **名称**                                        | **默认值**                    |
| ----------------------------------------------- | ----------------------------- |
| --cy-button-border-radius                       | @radius-default               |
| --cy-button-border-width                        | 4rpx                          |
| --cy-button-danger-active-bg-color              | @error-color-7                |
| --cy-button-danger-active-border-color          | @error-color-7                |
| --cy-button-danger-bg-color                     | @error-color                  |
| --cy-button-danger-border-color                 | @error-color                  |
| --cy-button-danger-color                        | @font-white-1                 |
| --cy-button-danger-dashed-border-color          | @button-danger-dashed-color   |
| --cy-button-danger-dashed-color                 | @error-color                  |
| --cy-button-danger-dashed-disabled-color        | @button-danger-disabled-color |
| --cy-button-danger-disabled-bg                  | @error-color-3                |
| --cy-button-danger-disabled-border-color        | @error-color-3                |
| --cy-button-danger-disabled-color               | @font-white-1                 |
| --cy-button-danger-outline-active-bg-color      | @bg-color-container-active    |
| --cy-button-danger-outline-active-border-color  | @error-color-7                |
| --cy-button-danger-outline-border-color         | @button-danger-outline-color  |
| --cy-button-danger-outline-color                | @error-color                  |
| --cy-button-danger-outline-disabled-color       | @error-color-3                |
| --cy-button-danger-text-active-bg-color         | @bg-color-container-active    |
| --cy-button-danger-text-color                   | @error-color                  |
| --cy-button-danger-text-disabled-color          | @button-danger-disabled-color |
| --cy-button-default-active-bg-color             | @bg-color-component-active    |
| --cy-button-default-active-border-color         | @bg-color-component-active    |
| --cy-button-default-bg-color                    | @bg-color-component           |
| --cy-button-default-border-color                | @bg-color-component           |
| --cy-button-default-color                       | @font-gray-1                  |
| --cy-button-default-disabled-bg                 | @bg-color-component-disabled  |
| --cy-button-default-disabled-border-color       | @bg-color-component-disabled  |
| --cy-button-default-disabled-color              | @font-gray-4                  |
| --cy-button-default-outline-active-bg-color     | @bg-color-container-active    |
| --cy-button-default-outline-active-border-color | @component-border             |
| --cy-button-default-outline-border-color        | @component-border             |
| --cy-button-default-outline-color               | @font-gray-1                  |
| --cy-button-default-outline-disabled-color      | @component-border             |
| --cy-button-default-text-active-bg-color        | @bg-color-container-active    |
| --cy-button-extra-small-font-size               | @font-size-base               |
| --cy-button-extra-small-height                  | 56rpx                         |
| --cy-button-extra-small-icon-font-size          | 36rpx                         |
| --cy-button-extra-small-padding-horizontal      | 16rpx                         |
| --cy-button-font-weight                         | 600                           |
| --cy-button-ghost-border-color                  | @button-ghost-color           |
| --cy-button-ghost-color                         | @bg-color-container           |
| --cy-button-ghost-danger-border-color           | @error-color                  |
| --cy-button-ghost-danger-color                  | @error-color                  |
| --cy-button-ghost-disabled-color                | rgba(255, 255, 255, 0.35)     |
| --cy-button-ghost-primary-border-color          | @brand-color                  |
| --cy-button-ghost-primary-color                 | @brand-color                  |
| --cy-button-icon-border-radius                  | 8rpx                          |
| --cy-button-icon-spacer                         | @spacer                       |
| --cy-button-large-font-size                     | @font-size-m                  |
| --cy-button-large-height                        | 96rpx                         |
| --cy-button-large-icon-font-size                | 48rpx                         |
| --cy-button-large-padding-horizontal            | 40rpx                         |
| --cy-button-light-active-bg-color               | @brand-color-light-active     |
| --cy-button-light-active-border-color           | @brand-color-light-active     |
| --cy-button-light-bg-color                      | @brand-color-light            |
| --cy-button-light-border-color                  | @brand-color-light            |
| --cy-button-light-color                         | @brand-color                  |
| --cy-button-light-disabled-bg                   | @brand-color-light            |
| --cy-button-light-disabled-border-color         | @brand-color-light            |
| --cy-button-light-disabled-color                | @brand-color-disabled         |
| --cy-button-light-outline-active-bg-color       | @brand-color-light-active     |
| --cy-button-light-outline-active-border-color   | @brand-color-active           |
| --cy-button-light-outline-bg-color              | @brand-color-light            |
| --cy-button-light-outline-border-color          | @button-light-outline-color   |
| --cy-button-light-outline-color                 | @brand-color                  |
| --cy-button-light-outline-disabled-color        | @brand-color-disabled         |
| --cy-button-light-text-active-bg-color          | @bg-color-container-active    |
| --cy-button-light-text-color                    | @brand-color                  |
| --cy-button-medium-font-size                    | @font-size-m                  |
| --cy-button-medium-height                       | 80rpx                         |
| --cy-button-medium-icon-font-size               | 40rpx                         |
| --cy-button-medium-padding-horizontal           | 32rpx                         |
| --cy-button-primary-active-bg-color             | @brand-color-active           |
| --cy-button-primary-active-border-color         | @brand-color-active           |
| --cy-button-primary-bg-color                    | @brand-color                  |
| --cy-button-primary-border-color                | @brand-color                  |
| --cy-button-primary-color                       | @font-white-1                 |
| --cy-button-primary-dashed-border-color         | @button-primary-dashed-color  |
| --cy-button-primary-dashed-color                | @brand-color                  |
| --cy-button-primary-dashed-disabled-color       | @brand-color-disabled         |
| --cy-button-primary-disabled-bg                 | @brand-color-disabled         |
| --cy-button-primary-disabled-border-color       | @brand-color-disabled         |
| --cy-button-primary-disabled-color              | @font-white-1                 |
| --cy-button-primary-outline-active-bg-color     | @bg-color-container-active    |
| --cy-button-primary-outline-active-border-color | @brand-color-active           |
| --cy-button-primary-outline-border-color        | @button-primary-outline-color |
| --cy-button-primary-outline-color               | @brand-color                  |
| --cy-button-primary-outline-disabled-color      | @brand-color-disabled         |
| --cy-button-primary-text-active-bg-color        | @bg-color-container-active    |
| --cy-button-primary-text-color                  | @brand-color                  |
| --cy-button-primary-text-disabled-color         | @brand-color-disabled         |
| --cy-button-small-font-size                     | @font-size-base               |
| --cy-button-small-height                        | 64rpx                         |
| --cy-button-small-icon-font-size                | 36rpx                         |
| --cy-button-small-padding-horizontal            | 24rpx                         |

![](/media/202406/IMG_4862_1719458484.JPG)