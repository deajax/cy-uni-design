## API

### 声明

|      参数       |      类型      |                             描述                             |    默认值    |
| :-------------: | :------------: | :----------------------------------------------------------: | :----------: |
|      name       | number、string |                  标签名称，作为匹配的标识符                  | 标签的索引值 |
|      title      |     string     |                             标题                             |      -       |
|    disabled     |    boolean     |                         是否禁用标签                         |    false     |
|       dot       |    boolean     |        是否在标题右上角显示小红点（优先级高于 badge）        |    false     |
|      badge      | number、string |                     图标右上角徽标的内容                     |      -       |
| badge-max-count | number、string | 徽标数最大数字限制,超过这个数字将变成 badgeMaxCount+,如果传空字符串则不设置 |      99      |
|   title-style   |     object     |                        自定义标题样式                        |      -       |
|   title-class   |     string     |                        自定义标题类名                        |      -       |
|    icon-type    |     string     | 图标图案，为 uniapp 扩展组件（uni-ui）下的 uni-icons 的 type 值，customPrefix 用法等同 |      -       |
|    icon-size    | number、string |                           图标大小                           |      16      |
|  custom-prefix  |     string     |                          自定义图标                          |      -       |
|    image-src    |     string     |                           图片路径                           |      -       |
|   image-mode    |     string     | 图片裁剪、缩放的模式，为 uniapp 内置组件->媒体组件—>image 下的 mode 属性的可选值 |      -       |
|    position     |     string     | 在有图标或图片的情况下，标题围绕它们所在的位置，可选值：left、top、bottom |    right     |

### 插槽

| 名称    | 描述       |
| ------- | ---------- |
| default | 标签页内容 |

### 外部样式类

| 类名        | 说明         |
| ----------- | ------------ |
| customClass | 跟节点样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |