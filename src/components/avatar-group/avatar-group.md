## 代码演示

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



## API

### 声明

| 名称            | 类型          | 默认值    | 说明                                                         | 必传 |
| :-------------- | :------------ | :-------- | :----------------------------------------------------------- | :--- |
| cascading       | String        | 'left-up' | 图片之间的层叠关系，可选值：左侧图片在上和右侧图片在上。可选项：left-up/right-up。 | N    |
| collapse-avatar | String / Slot | -         | 头像数量超出时，会出现一个头像折叠元素。该元素内容可自定义。默认为 `+N`。示例：`+5`，`...`, `更多` | N    |
| max             | Number        | -         | 能够同时显示的最多头像数量                                   | N    |
| size            | String        | medium    | 尺寸，示例值：small/medium/large。优先级低于 Avatar.size     |      |

### 插槽

| 名称            | 描述                     |
| --------------- | ------------------------ |
| default         | 默认插槽，用于自定义样式 |
| collapse-avatar | 自定义折叠元素           |

### 外部样式类

| 类名                 | 说明 |
| -------------------- | ---- |
| custom-class         |      |
| custom-class-image   |      |
| custom-class-content |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |