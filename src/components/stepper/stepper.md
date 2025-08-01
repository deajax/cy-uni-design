## 代码演示

#### 基础步进器

```vue
<cy-stepper />
```

#### 最大最小状态

```vue
<cy-stepper default-value="0" />
<cy-stepper default-value="5" min="5" />
<cy-stepper default-value="99" min="5" max="99" />
```

#### 禁用状态

```vue
<cy-stepper theme="filled" disabled />
<cy-stepper theme="outline" disabled />
<cy-stepper disabled />
```

#### 步进器样式

```vue
<cy-stepper theme="filled" />
<cy-stepper theme="outline" />
<cy-stepper />
```

#### 步进器尺寸

```vue
<cy-stepper theme="filled" size="large" />
<cy-stepper theme="filled" />
<cy-stepper theme="filled" size="small" />
```



## API

### 声明

| 名称          | 类型            | 默认值    | 说明                                 | 必传 |
| :------------ | :-------------- | :-------- | :----------------------------------- | :--- |
| disable-input | Boolean         | false     | 禁用输入框                           | N    |
| disabled      | Boolean         | false     | 禁用全部操作                         | N    |
| input-width   | Number          | -         | 输入框宽度，默认单位 `px`            | N    |
| max           | Number          | 100       | 最大值                               | N    |
| min           | Number          | 0         | 最小值                               | N    |
| step          | Number          | 1         | 步长                                 | N    |
| size          | String          | medium    | 组件尺寸。可选项：small/medium/large | N    |
| value         | String / Number | 0         | 值                                   | N    |
| default-value | String / Number | undefined | 值。非受控属性                       | N    |

### 事件

| 名称      | 参数                           | 描述                 |
| :-------- | :----------------------------- | :------------------- |
| blur      | `({ type: string | number })`  | 输入框失去焦点时触发 |
| change    | `({ value: string | number })` | 数值发生变更时触发   |
| overlimit | `({type: 'minus' | 'plus'})`   | 数值超出限制时触发   |

### 外部样式类

| 类名               | 说明             |
| :----------------- | :--------------- |
| custom-class       | 根节点样式类     |
| custom-class-input | 输入框样式类     |
| custom-class-minus | 左侧递减号样式类 |
| custom-class-plus  | 右侧递增号样式类 |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |