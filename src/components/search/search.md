## 代码演示

#### 基础搜索框

```vue
<cy-search v-model="search" placeholder="请输入搜索内容"></cy-search>
```

#### 搜索框形状

```vue
<cy-search v-model="search" placeholder="请输入搜索内容" shape="round"></cy-search>
```

#### 带取消按钮

```vue
<cy-search v-model="search" placeholder="请输入搜索内容" action="取消" @action-click="onActionClick" />
```

#### 禁用输入框

```vue
<cy-search v-model="search" placeholder="禁用输入框" shape="round" disabled />
```

#### 自定义内容

```vue
<cy-search>
  <template #input>
		自定义内容
  </template>
</cy-search>
```



## API

### 声明

| 名称              | 类型          | 默认值                | 说明                                                         | 必传 |
| :---------------- | :------------ | :-------------------- | :----------------------------------------------------------- | :--- |
| action            | String / Slot | ''                    | 自定义右侧操作按钮文字                                       | N    |
| disabled          | Boolean       | false                 | 是否禁用                                                     | N    |
| focus             | Boolean       | false                 | 是否聚焦                                                     | N    |
| confirm-type      | String        | search                | 设置键盘右下角按钮的文字，仅在type='text'时生效。 具体释义： `send` 右下角按钮为“发送”； `search` 右下角按钮为“搜索”； `next` 右下角按钮为“下一个”； `go` 右下角按钮为“前往”； `done` 右下角按钮为“完成”。 [小程序官方文档](https://developers.weixin.qq.com/miniprogram/dev/component/input.html)。可选项：send/search/next/go/done | N    |
| hold-keyboard     | Boolean       | false                 | focus时，点击页面的时候不收起键盘                            | N    |
| placeholder-style | String        | -                     | 必需。指定 placeholder 的样式                                | Y    |
| placeholder-class | String        | input-placeholder     | 指定 placeholder 的样式类                                    | N    |
| left-icon         | String / Slot | 'search'              | 左侧图标                                                     | N    |
| placeholder       | String        | ''                    | 占位符                                                       | N    |
| right-icon        | String / Slot | 'close-circle-filled' | 已废弃。右侧图标                                             | N    |
| clearable         | Boolean       | true                  | 是否启用清除控件                                             | N    |
| shape             | String        | 'square'              | 搜索框形状。可选项：square/round                             | N    |
| value             | String        | ''                    | 值                                                           | N    |
| type              | String        | 'text'                | 拉起键盘的类型，可选项：text/number/idcard/digit/nickname    | N    |

### 插槽

| 名称      | 描述             |
| --------- | ---------------- |
| default   | 右侧区域         |
| left-icon | 左侧搜索图标区域 |
| action    | 右侧操作区域     |
| input     | 输入框区域       |

### 事件

| 名称          | 参数                | 描述                       |
| ------------- | ------------------- | -------------------------- |
| @change       | ({ value: string }) | 值发生变化时触发           |
| @clear        | ({ value: string }) | 点击清除时触发             |
| @action-click | ({})                | 点击右侧操作按钮文字时触发 |
| @focus        | ({ value: string }) | 聚焦时触发                 |
| @blur         | ({ value: string }) | 失去焦点时触发             |
| @submit       | ({ value: string }) | 提交时触发                 |

### 外部样式类

| 类名                    | 说明 |
| ----------------------- | ---- |
| custom-class            |      |
| custom-class-left-icon  |      |
| custom-class-content    |      |
| custom-class-input      |      |
| custom-class-clearable  |      |
| custom-class-action     |      |
| custom-class-right-icon |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |