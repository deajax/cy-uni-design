## 代码演示

#### 基础用法

```vue
<cy-checkbox v-model="checked">复选框</cy-checkbox>
```

```js
export default {
	data() {
		return {
      checked: true,
    }
  }
}
```



#### 自定义颜色

```vue
<view style="--cy-brand-color: red">
  <cy-checkbox v-model="checked" primaryColor="#00a231">自定义颜色</cy-checkbox>
</view>
```

```js
export default {
	data() {
		return {
      checked: true,
    }
  }
}
```



#### 自定义图标

```vue
<cy-checkbox icon="lock-line" v-model="checked">自定义图标</cy-checkbox>
```

```js
export default {
	data() {
		return {
      checked: true,
    }
  }
}
```



#### 完全自定义图标

```vue
<cy-checkbox v-model="checked">
			完全自定义图标
  <template slot="icon">
		<image v-if="checked" style="width: 24px;height: 24px;display: block;" src="/static/logo.png" />
		<image v-else style="width: 24px;height: 24px;display: block; opacity: .4;" src="/static/logo.png" />
  </template>
</cy-checkbox>
```

```js
export default {
	data() {
		return {
      checked: true,
    }
  }
}
```



#### 禁用

```vue
<cy-checkbox v-model="disabledChecked" :disabled="true">禁用选中</cy-checkbox>
<cy-checkbox v-model="disabledUnChecked" :disabled="true">禁用不选中</cy-checkbox>
```

```js
export default {
	data() {
		return {
      disabledChecked: true,
			disabledUnChecked: false,
    }
  }
}
```



#### 横向多选框

```vue
<cy-checkbox-group custom-class="box" borderless @change="onGroupChange" v-model="box">
  <cy-checkbox :name="i" v-for="i in 3" :key="i">标题标题</cy-checkbox>
</cy-checkbox-group>
```

```js
export default {
	data() {
		return {
      box: 0,
    }
  },
  methods: {
		onGroupChange(e) {
			console.log(e)
		},
  }
}
```



#### 复选框组

```vue
<cy-checkbox-group ref="cGroup" @change="onGroupChange" v-model="color4">
  <view v-for="item in colorList" :key="item.value">
    <cy-checkbox :name="item.value">{{ item.label }}</cy-checkbox>
  </view>
</cy-checkbox-group>
```

```js
export default {
	data() {
		return {
      color4: null,
    }
  },
  methods: {
		onGroupChange(e) {
			console.log(e)
		},
  }
}
```



#### 全选，反选，清空

```vue
<view class="button-group">
  <button @tap="selectAll">全选</button>
  <button @tap="selectReverse">反选</button>
  <button @tap="clearAll">清空</button>
</view>

<cy-checkbox-group ref="cGroup" @change="onGroupChange" v-model="color4">
  <view v-for="item in colorList" :key="item.value">
    <cy-checkbox :name="item.value">{{ item.label }}</cy-checkbox>
  </view>
</cy-checkbox-group>
```

```js
export default {
	data() {
		return {
      color4: null,
    }
  },
  methods: {
		onGroupChange(e) {
			console.log(e)
		},
    selectAll() {
			this.$refs.cGroup.selectAll()
			console.log(this.color4)
		},
		selectReverse() {
			this.$refs.cGroup.selectReverse()
			console.log(this.color4)
		},
		clearAll() {
			this.$refs.cGroup.clearAll()
			console.log(this.color4)
		},
  }
}
```



#### 勾选框位置

```vue
<cy-checkbox v-model="checked">复选框</cy-checkbox>
<cy-checkbox v-model="checked" placement="right">复选框</cy-checkbox>
```

```js
export default {
	data() {
		return {
      checked: true,
    }
  }
}
```



## API

### checkbox 声明

| 名称          | 类型    | 默认值 | 说明                                                         | 必传 |
| ------------- | ------- | ------ | ------------------------------------------------------------ | ---- |
| v-model       | boolean | false  | 是否选中                                                     | N    |
| label         | string  | -      | 主文案                                                       | N    |
| content       | String  | -      | 单选内容                                                     | N    |
| disabled      | boolean | false  | 是否禁用                                                     | N    |
| icon          | string  | -      | 自定义图标                                                   | N    |
| prevent-click | boolean |        | 阻止内部的点击事件，只在自定义样式由外部触发toggle事件时设置为true | N    |
| placement     | String  | left   | 复选框和内容相对位置。可选项：left/right                     | N    |
| block         | Boolean | true   | 是否为块级元素                                               | N    |
| borderless    | Boolean | false  | 是否开启无边框模式                                           | N    |

### checkbox-group 声明

| 名称     | 类型    | 默认值 | 说明           | 必传 |
| -------- | ------- | ------ | -------------- | ---- |
| v-model  | array   | -      | 是否选中       | N    |
| disabled | boolean | false  | 是否禁用       | N    |
| max      | string  | -      | 最多选中的个数 | N    |



### checkbox 插槽

| 名称    | 参数 | 描述                         |
| ------- | ---- | ---------------------------- |
| default | -    | 默认插槽，位于label上方      |
| icon    | -    | 自定义选中图标和非选中图标。 |
| label   | -    | 自定义主文案内容             |

### checkbox-group 插槽

| 名称    | 参数 | 描述     |
| ------- | ---- | -------- |
| default | -    | 默认插槽 |



### checkbox 事件

| 名称   | 参数             | 描述             |
| ------ | ---------------- | ---------------- |
| change | 更新后的选中状态 | 选中状态发生变更 |

### checkbox-group 事件

| 名称   | 参数                  | 描述             |
| ------ | --------------------- | ---------------- |
| change | 更新后选中值的label组 | 选中状态发生变更 |



### checkbox方法

| 方法名 | 说明                                                         | 参数 |
| :----- | :----------------------------------------------------------- | :--- |
| toggle | 切换复选框的选中状态，一般配合prevent-click属性使用来自定义样式 | -    |

### checkbox-group 方法

| 方法名        | 说明                                       | 参数 |
| :------------ | :----------------------------------------- | :--- |
| selectAll     | 全选，注意主动调用该方法不会触发change事件 | -    |
| selectReverse | 反选，注意主动调用该方法不会触发change事件 | -    |
| clearAll      | 清空，注意主动调用该方法不会触发change事件 | -    |



### checkbox 外部样式类

| 类名                     | 说明         |
| ------------------------ | ------------ |
| custom-class             | 根节点样式类 |
| custom-class-icon        | 图标样式类   |
| custom-class-content     | 内容样式类   |
| custom-class-label       | 标签样式类   |
| custom-class-description | 描述样式类   |

### checkbox-group 外部样式类

| 类名         | 说明         |
| ------------ | ------------ |
| custom-class | 根节点样式类 |



### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |