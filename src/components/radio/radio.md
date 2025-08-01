## 代码演示

#### 基础演示

```vue
<cy-radio v-model="baseValue" name="base1">基础用法1</cy-radio>
<cy-radio v-model="baseValue" name="base2">基础用法2</cy-radio>
```

```js
export default {
	data() {
		return {
      baseValue: 'base1',
    }
  }
}
```

#### 自定义颜色

```vue
<view style="--cy-brand-color: red">
  <cy-radio v-model="baseValue" name="base1">自定义颜色1</cy-radio>
  <cy-radio v-model="baseValue" name="base2">自定义颜色2</cy-radio>
</view>
```

```js
export default {
	data() {
		return {
      baseValue: 'base1',
    }
  }
}
```

#### 自定义图标

```vue
<cy-radio v-model="baseValue" icon="lock-line" name="base1">自定义图标1</cy-radio>
<cy-radio v-model="baseValue" icon="lock-line" name="base2">自定义图标2</cy-radio>
```

```js
export default {
	data() {
		return {
      baseValue: 'base1',
    }
  }
}
```

#### 完全自定义图标

```vue
<cy-radio v-model="iconValue" name="icon1">
  <text>完全自定义图标1</text>
  <template slot="icon">
<text :style="{ color: iconValue === 'icon1' ? '#f00' : '#ccc' }">1</text>
  </template>
</cy-radio>
<cy-radio v-model="iconValue" name="icon2">
  <text>完全自定义图标2</text>
  <template slot="icon">
<text :style="{ color: iconValue === 'icon2' ? '#f00' : '#ccc' }">2</text>
  </template>
</cy-radio>
```

```js
export default {
	data() {
		return {
      iconValue: 'icon1',
    }
  }
}
```

#### 自定义大小

```vue
<cy-radio v-model="baseValue" :iconSize="30" :titleStyle="{ 'font-size': '22px', color: 'red' }"
          name="base1">自定义大小1</cy-radio>
<cy-radio v-model="baseValue" :iconSize="30" :titleStyle="{ 'font-size': '22px', color: 'red' }"
          name="base2">自定义大小2</cy-radio>
```

```js
export default {
	data() {
		return {
      baseValue: 'base1',
    }
  }
}
```

#### 禁用

```vue
<cy-radio v-model="disabledValue" :disabled="true" name="disabled1">禁用1</cy-radio>
<cy-radio v-model="disabledValue" :disabled="true" name="disabled2">禁用2</cy-radio>
```

```js
export default {
	data() {
		return {
      disabledValue: 'disabled1',
    }
  }
}
```

#### 横向单选框

```vue
<cy-radio-group custom-class="box" borderless @change="onGroupChange" v-model="baseValue">
  <view v-for="item in 3" :key="item">
    <cy-radio :name="item">标题标题</cy-radio>
  </view>
</cy-radio-group>
```

```js
export default {
	data() {
		return {
      baseValue: 0,
    }
  },
  methods: {
    onGroupChange(e) {
			console.log(e)
		},
  }
}
```

#### 单选框组

```vue
<cy-radio-group @change="onGroupChange" v-model="color">
  <view v-for="item in colorList" :key="item.value">
    <cy-radio :name="item.name">{{ item.label }}</cy-radio>
  </view>
</cy-radio-group>
```

```js
export default {
	data() {
		return {
      color: 'red',
      colorList: [{
				label: '红色',
				name: 'red'
			}, {
				label: '绿色',
				name: 'green'
			}, {
				label: '蓝色',
				name: 'blue'
			}, {
				label: '粉色',
				name: 'pink'
			}, {
				label: '黑色',
				name: 'black'
			}]
    }
  },
  methods: {
    onGroupChange(e) {
			console.log(e)
		},
  }
}
```

#### 选中项可以取消

```vue
<cy-radio-group @change="onGroupChange" v-model="colorClear">
  <view v-for="item in colorList" :key="item.value">
    <cy-radio clearable :name="item.name">{{ item.label }}</cy-radio>
  </view>
</cy-radio-group>
```

```js
export default {
	data() {
		return {
      colorClear: 'red',
      colorList: [{
				label: '红色',
				name: 'red'
			}, {
				label: '绿色',
				name: 'green'
			}, {
				label: '蓝色',
				name: 'blue'
			}, {
				label: '粉色',
				name: 'pink'
			}, {
				label: '黑色',
				name: 'black'
			}]
    }
  },
  methods: {
    onGroupChange(e) {
			console.log(e)
		},
  }
}
```

#### 勾选框位置

```vue
<cy-radio v-model="baseValue" name="base1">基础用法</cy-radio>
<cy-radio v-model="baseValue" name="base2" placement="right">勾选框在右侧</cy-radio>
```

```js
export default {
	data() {
		return {
      baseValue: 'base1',
    }
  }
}
```

## API

### radio 声明

| 名称          | 类型                      | 默认值 | 说明                                                         | 必传   |
| :------------ | :------------------------ | :----- | :----------------------------------------------------------- | :----- |
| v-model/value | String / Number / Boolean | -      | 单选按钮的值。                                               | number |
| name          | String / Number / Boolean | -      | HTML 元素原生属性                                            | N      |
| icon          | String                    | -      | 自定义图标。                                                 | N      |
| label         | String                    | -      | 主文案                                                       | N      |
| content       | String                    | -      | 单选内容                                                     | N      |
| disabled      | Boolean                   | false  | 是否为禁用态                                                 | N      |
| prevent-click | Boolean                   | false  | 阻止内部的点击事件，只在自定义样式由外部触发select事件时设置为true | N      |
| clearable     | Boolean                   | false  | 选中的选项再次点击能否取消选中                               | N      |
| placement     | String                    | 'left' | 复选框和内容相对位置。可选项：left/right                     | N      |
| block         | Boolean                   | true   | 是否为块级元素                                               | N      |
| borderless    | Boolean                   | false  | 是否开启无边框模式                                           | N      |

### radio-group 声明

| 名称          | 类型                  | 默认值 | 说明                 | 必传 |
| :------------ | :-------------------- | :----- | :------------------- | :--- |
| v-model/value | string/number/boolean | -      | 选中的值。           | N    |
| disabled      | Boolean               | false  | 是否禁用全部子单选框 | N    |
| borderless    | Boolean               | false  | 是否开启无边框模式   | N    |



### radio 插槽

| 名称    | 参数 | 描述                         |
| ------- | ---- | ---------------------------- |
| default | -    | 默认插槽，位于label上方      |
| icon    | -    | 自定义选中图标和非选中图标。 |
| label   | -    | 自定义主文案内容             |
| content | -    | 自定义单选内容               |

### radio-group 插槽

| 名称    | 参数 | 描述     |
| ------- | ---- | -------- |
| default | -    | 默认插槽 |



### radio 事件

| 名称   | 参数 | 描述                                                     |
| ------ | ---- | -------------------------------------------------------- |
| select | -    | 选择当前radio，一般配合prevent-click属性使用来自定义样式 |

### radio-group 事件

| 名称   | 参数         | 描述             |
| ------ | ------------ | ---------------- |
| change | 新的选中的值 | 选中的值发生变化 |



### radio 外部样式类

| 类名                     | 说明 |
| ------------------------ | ---- |
| custom-class             |      |
| custom-class-icon        |      |
| custom-class-conetnt     |      |
| custom-class-title       |      |
| custom-class-description |      |

### radio-group 外部样式类

| 类名         | 说明 |
| ------------ | ---- |
| custom-class |      |

