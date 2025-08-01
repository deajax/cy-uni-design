## 代码演示

#### 图片头像

```vue
<cy-avatar :image="image" />
<cy-avatar shape="round" :image="image" />
```

#### 字符头像

```vue
<cy-avatar>A</cy-avatar>
<cy-avatar shape="round">A</cy-avatar>
```

#### 图标头像

```vue
<cy-avatar icon="user-line" />
<cy-avatar shape="round" icon="user-line" />
```

#### 组合头像

```vue
<view class="avatar-example">
  <cy-avatar-group max="5" collapseAvatar="+5">
    <cy-avatar v-for="i in 5" :key="i" :image="image" bordered />
  </cy-avatar-group>
</view>
<view class="avatar-example">
  <cy-avatar-group max="5" cascading="right-up">
    <cy-avatar v-for="i in 5" :key="i" :image="image" bordered />
  </cy-avatar-group>
</view>
```

#### 徽标头像

```vue
<cy-avatar :image="image" :badge-props="{ dot: true }" />
<cy-avatar :badge-props="{ count: 8 }">A</cy-avatar>
<cy-avatar icon="user-line" :badge-props="{ count: 12 }" />
```

#### 头像尺寸

```vue
<view class="avatar-example">
  <cy-avatar :image="image" size="large" />
  <cy-avatar size="large">A</cy-avatar>
  <cy-avatar icon="user-line" size="large" />
</view>

<view class="avatar-example">
  <cy-avatar :image="image" />
  <cy-avatar size="medium">A</cy-avatar>
  <cy-avatar icon="user-line" size="medium" />
</view>

<view class="avatar-example">
  <cy-avatar :image="image" size="small" />
  <cy-avatar size="small">A</cy-avatar>
  <cy-avatar icon="user-line" size="small" />
</view>
```



## API

### 声明

| 名称                    | 类型             | 默认值    | 说明                                                         | 必传 |
| :---------------------- | :--------------- | :-------- | :----------------------------------------------------------- | :--- |
| adjust-position         | Boolean          | true      | 键盘弹起时，是否自动上推页面                                 | N    |
| autofocus               | Boolean          | false     | 自动聚焦，拉起键盘                                           | N    |
| autosize                | Boolean / Object | false     | 是否自动增高，值为 true 时，style.height 不生效。支持传入对象，如 | N    |
| confirm-hold            | Boolean          | false     | 点击键盘右下角按钮时是否保持键盘不收起点                     | N    |
| confirm-type            | String           | return    | 设置键盘右下角按钮的文字，仅在 type='text'时生效。可选项：return/send/search/next/go/done | N    |
| cursor-spacing          | Number           | 0         | 指定光标与键盘的距离。取textarea距离底部的距离和cursor-spacing指定的距离的最小值作为光标与键盘的距离 | N    |
| disabled                | Boolean          | false     | 是否禁用文本框                                               | N    |
| focus                   | Boolean          | false     | 自动聚焦                                                     | N    |
| label                   | String / Slot    | -         | 左侧文本                                                     | N    |
| maxcharacter            | Number           | -         | 用户最多可以输入的字符个数，一个中文汉字表示两个字符长度     | N    |
| maxlength               | Number           | -1        | 用户最多可以输入的字符个数。默认为 -1，不限制输入长度        | N    |
| indicator               | Boolean          | false     | 显示文本计数器，如 0/140。当 `maxlength < 0 && maxcharacter < 0` 成立时， indicator无效 | N    |
| placeholder             | String           | undefined | 占位符                                                       | N    |
| placeholderStyle        | String           | ''        | 指定 placeholder 的样式，目前仅支持 color ,font-size和font-weight | N    |
| value                   | String           | null      | 文本框值                                                     | N    |
| default-value           | String           | ''        | 文本框值。非受控属性                                         | N    |
| fixed                   | Boolean          | false     | 如果 textarea 是在一个 `position:fixed` 的区域，需要显示指定属性 fixed 为 true | N    |
| bordered                | Boolean          | false     | 是否显示外边框                                               | N    |
| cursor                  | Number           | -1        | 指定 focus 时的光标位置                                      | N    |
| disable-default-padding | Boolean          | false     | 是否去掉 iOS 下的默认内边距                                  | N    |
| show-confirm-bar        | Boolean          | true      | 是否显示键盘上方带有”完成“按钮那一栏                         | N    |
| selection-start         | Number           | -1        | 光标起始位置，自动聚集时有效，需与 selection-end 搭配使用    | N    |
| selection-end           | Number           | -1        | 光标结束位置，自动聚集时有效，需与 selection-start 搭配使用  | N    |
| hold-keyboard           | Boolean          | false     | focus时，点击页面的时候不收起键盘                            | N    |

### 插槽

| 名称    | 描述             |
| ------- | ---------------- |
| default | 默认插槽，在底部 |
| label   | 左侧文本插槽     |

### 事件

| 名称                 | 参数                                     | 描述                             |
| :------------------- | :--------------------------------------- | :------------------------------- |
| blur                 | `(value: TextareaValue, cursor: number)` | 失去焦点时触发                   |
| change               | `(value: TextareaValue, cursor: number)` | 输入内容变化时触发               |
| enter                | `(value: TextareaValue)`                 | 点击完成时触发                   |
| focus                | `(value: TextareaValue)`                 | 获得焦点时触发                   |
| line-change          | `(value: TextareaValue)`                 | 行高发生变化时触发               |
| keyboardheightchange | `(height: number, duration: number)`     | 键盘高度发生变化的时候触发此事件 |

### 外部样式类

| 类名                   | 说明 |
| ---------------------- | ---- |
| custom-class           |      |
| custom-class-label     |      |
| custom-class-wrapper   |      |
| custom-class-indicator |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |