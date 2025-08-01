## Grid-item API

### 声明

| 名称        | 类型            | 默认值      | 说明                                                         | 必传 |
| :---------- | :-------------- | :---------- | :----------------------------------------------------------- | :--- |
| badge-props | Object          | null        | 透传至 Badge 属性。支持dot/count/color                       | N    |
| description | String / Slot   | -           | 文本以外的更多描述，辅助信息。可以通过 Props 传入文本，也可以自定义标题节点 | N    |
| icon        | String / Object | -           | 图标名称。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon` | N    |
| image       | String / Slot   | -           | 图片，可以是图片地址，也可以自定义图片节点，值为 slot 的时候才能使用插槽 | N    |
| image-props | Object          | -           | 透传至 Image 组件                                            | N    |
| jump-type   | String          | navigate-to | 链接跳转类型。可选项：redirect-to/switch-tab/relaunch/navigate-to | N    |
| layout      | String          | vertical    | 内容布局方式。可选项：vertical/horizontal                    | N    |
| text        | String / Slot   | -           | 文本，可以通过 Props 传入文本，也可以自定义标题节点          | N    |
| url         | String          | -           | 点击后的跳转链接                                             | N    |

### 插槽

| 名称        | 描述                          |
| ----------- | ----------------------------- |
| default     | 默认插槽，在内容顶部          |
| image       | 图片下方                      |
| icon        | 图标下方                      |
| badge       | badge内部，用于自定义徽标内容 |
| text        | 文本下方                      |
| description | 描述下方                      |

### 事件

| 名称   | 参数    | 描述           |
| ------ | ------- | -------------- |
| @click | `event` | 点击子项后触发 |

### 外部样式类

| 类名                   | 说明 |
| ---------------------- | ---- |
| customClass            |      |
| customClassContent     |      |
| customClassImage       |      |
| customClassText        |      |
| customClassDescription |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |