## 代码演示

#### 状态类型

```
<cy-empty image="default" description="默认状态" />
<cy-empty image="item" description="暂无商品" />
<cy-empty image="search" description="没有找到你想要的结果" />
<cy-empty image="network" description="网络无法连接" />
<cy-empty image="list" description="暂无订单记录" />
```

#### 自定义图标

```
<cy-empty description="数据加载中">
  <template #icon>
 	 <cy-loading />
  </template>
</cy-empty>
```



## API

### 声明

| 名称        | 类型            | 默认值 | 说明                                                         | 必传 |
| :---------- | :-------------- | :----- | :----------------------------------------------------------- | :--- |
| action      | Slot            | -      | 操作按钮                                                     | N    |
| description | String / Slot   | -      | 描述文字                                                     | N    |
| icon        | String / Object | -      | 图标名称。值为字符串表示图标名称，值为 `Object` 类型，表示透传至 `icon`。 | N    |
| image       | String / Slot   | -      | 图片地址/类型。可选项：default/search/network/list/item      |      |

### 插槽

| 名称        | 描述     |
| ----------- | -------- |
| icon        | 图标下方 |
| image       | 图片下方 |
| description | 描述下方 |
| action      | 操作按钮 |

### 外部样式类

| 类名                     | 说明           |
| :----------------------- | :------------- |
| custom-class             | 根节点样式类   |
| custom-class-description | 描述样式类     |
| custom-class-image       | 图片样式类     |
| custom-class-icon        | 图标样式类     |
| custom-class-actions     | 操作按钮样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称                               | 默认值          | 描述 |
| :--------------------------------- | :-------------- | :--- |
| --cy-empty-action-margin-top       | $spacer-4       | -    |
| --cy-empty-description-color       | $font-gray-3    | -    |
| --cy-empty-description-font-size   | $font-size-base | -    |
| --cy-empty-description-line-height | 44rpx           | -    |
| --cy-empty-description-margin-top  | $spacer-2       | -    |
| --cy-empty-icon-color              | $font-gray-3    | -    |