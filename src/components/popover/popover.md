## 代码演示

#### 基础用法

```vue
<cy-popover content="popover">
  <cy-button>点我</cy-button>
</cy-popover>
```

#### 自定义颜色

```vue
<cy-popover background="red" color="#fff" content="popover">
  <cy-button>点我</cy-button>
</cy-popover>
```

#### 自定义位置

```vue
<cy-row :gutter="8" :gap="32">
  <cy-col :span="item == 'left' ? 12 : 8" v-for="item in placements" :key="item"
          :custom-class="item == 'left' ? 'align-right' : ''">
    <cy-popover :placement="item">
      <cy-button size="small">{{ item }}</cy-button>
      <template #content>
        <cy-cell left-icon="qr-scan-line" title="扫一扫" />
        <cy-cell left-icon="exchange-cny-fill" title="付钱/收钱" />
        <cy-cell left-icon="qr-code-line" title="乘车码" />
        <cy-cell left-icon="user-add-line" title="添加朋友" :bordered="false" />
      </template>
    </cy-popover>
  </cy-col>
</cy-row>
```

```js
<script>
export default {
	components: {},
	data() {
		return {
			placements: [
				'top-left',
				'top',
				'top-right',
				'left',
				'right',
				'bottom-left',
				'bottom',
				'bottom-right',
			],
		}
	},
}
</script>
```



## API

### 声明

| 名称       | 类型    | 默认值 | 说明                                                         | 必传        |
| :--------- | :------ | :----- | :----------------------------------------------------------- | :---------- |
| background | String  | -      | 弹出框背景颜色                                               | N           |
| color      | String  | -      | 弹出框文字颜色                                               | N           |
| content    | String  | -      | 弹出内容                                                     | String/slot |
| placement  | String  | top    | 弹出方向，可选`top`/`top-left`/`top-right`/`left`/`right`/`bottom`/`bottom-left`/`bottom-right` | N           |
| visible    | Boolean | false  | 是否显示                                                     | N           |

### 插槽

| 名称    | 参数 | 描述                                |
| ------- | ---- | ----------------------------------- |
| default | -    | 默认插槽，用来放置弹出按钮          |
| content | -    | 弹出内容插槽，位于`content`声明下方 |

### 事件

| 名称 | 参数 | 描述 |
| ---- | ---- | ---- |
|      |      |      |

### 外部样式类

| 类名                 | 说明 |
| -------------------- | ---- |
| custom-class         |      |
| custom-class-content |      |

