### 使用示例

```vue
<template>
    <cy-description 
        :icon="{ name: 'star', size: '24px', color: 'red' }" 
        label="用户名" 
        content="张三" 
        size="large" 
        jumpType="navigateTo" 
        url="/pages/user/profile"
        @click="handleDescriptionClick"
    />
</template>

<script>
export default {
    methods: {
        handleDescriptionClick(event) {
            console.log('Description clicked:', event);
        }
    }
};
</script>
```



## API

### 声明

| 属性名   | 类型          | 默认值     | 描述                                                         |
| :------- | :------------ | :--------- | :----------------------------------------------------------- |
| icon     | String/Object | -          | 图标名称或对象，对象格式为 `{ name: 'icon-name', size: '16px', color: '#000' }` |
| label    | null/String   | -          | 标签文本，若不为空则显示 `label：`                           |
| content  | null/String   | -          | 内容文本，若不为空则直接显示                                 |
| size     | String        | `'middle'` | 组件大小，可选值为 `small`, `middle`, `large`                |
| jumpType | String        | -          | 页面跳转类型，可选值为 `navigateTo`, `switchTab`, `reLaunch`, `redirectTo` |
| url      | String        | -          | 跳转链接地址                                                 |



### 插槽（Slots）

| 插槽名  | 描述                                    |
| :------ | :-------------------------------------- |
| icon    | 自定义图标内容，优先级高于 `icon` 属性  |
| label   | 自定义标签内容，优先级高于 `label` 属性 |
| content | 自定义内容，优先级高于 `content` 属性   |
| default | 默认插槽，用于补充内容                  |
| extra   | 额外内容，通常用于右侧扩展              |



### 事件（Events）

| 事件名 | 参数  | 描述                 |
| :----- | :---- | :------------------- |
| @click | event | 当用户点击组件时触发 |



### **外部样式类（Custom Class）**

| customClass        | String/Array  | `''` | 自定义类名，应用于整个组件 |
| :----------------- | :------------ | :--- | :------------------------- |
| customClassIcon    | String/Array  | `''` | 自定义图标区域类名         |
| customClassLabel   | String/Array  | `''` | 自定义标签区域类名         |
| customClassContent | String/Array  | `''` | 自定义内容区域类名         |
| customStyle        | String/Object | `''` | 自定义样式，应用于整个组件 |
| customStyleLabel   | String/Object | `''` | 自定义标签区域样式         |

### 方法（Methods）

##### handleTap(event)

- 参数：
  - `event`: 触发点击事件的对象
- 描述：
  - 处理点击事件，触发 `click` 事件并根据 `jumpType` 和 `url` 进行页面跳转。