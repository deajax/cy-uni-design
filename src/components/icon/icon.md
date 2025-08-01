## 说明

> 图标库默认使用RemixIcon4.2.0图标库，版本随图标库更新。
>
> 使用时无需加“ri-”前缀。直接官网内复制图标名即可



## 代码演示

#### 基础样式

```
<cy-icon name="add-line"></view>
```

#### 颜色与尺寸

> 尺寸默认使用rpx数值，暂无法识别其他单位

```
<cy-icon name="add-line" color="#333" size="48"></view>
```

#### 自定义图标

> prefix与name之间没有空格，如需加空格请额外加到prefix里

```
<cy-icon prefix="iconfont" name="custom-icon"></view>
```



## API

### 声明

| 属性   | 值类型 | 默认值 | 必传 | 说明                       |
| :----- | :----- | :----- | :--- | :------------------------- |
| name   | String | -      | Y    | 图标名称                   |
| size   | String | -      | N    | 图标大小, 默认单位是 `rpx` |
| color  | String | -      | N    | 图标颜色                   |
| prefix | String | -      | N    | 自定义图标前缀             |

### 事件

| 名称      | 参数    | 描述           |
| --------- | ------- | -------------- |
| **click** | `event` | 点击图标时触发 |

### 外部样式类

| 类名        | 说明 |
| ----------- | ---- |
| customClass |      |
| customStyle |      |

### 插槽

| 名称    | 描述     |
| ------- | -------- |
| default | 图标后方 |