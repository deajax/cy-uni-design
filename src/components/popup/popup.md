## 代码演示

#### 顶部弹出

```vue
<cy-button variant="outline" block @click="showTop">
  顶部弹出
</cy-button>

<cy-popup ref="top" type="top">
  <view style="padding: 16px;">123</view>
  <view style="padding: 16px;">123</view>
  <view style="padding: 16px;">123</view>
</cy-popup>
```

```js
export default {
  methods: {
    showTop() {
      this.$refs.top.open("top");
    },
  },
};
```

#### 带标题和关闭按钮

```vue
<cy-button variant="outline" block @click="$refs.bottom.open('bottom')">
  底部弹出
</cy-button>

<cy-popup ref="bottom" type="bottom" title="底部弹出" close-btn>
  <view style="padding: 16px;">123</view>
  <view style="padding: 16px;">123</view>
  ......
  <view @click="$refs.bottom.close()">关闭</view>
</cy-popup>
```

#### 弹出方向

```vue
<cy-popup ref="show" :type="placement">
  <view style="padding: 16px;">123</view>
  <view style="padding: 16px;">123</view>
  <view style="padding: 16px;">123</view>
</cy-popup>
```

```js
export default {
  data() {
    return {
      placement: "top | right | bottom | left",
    };
  },
  methods: {
    onClick() {
      this.$refs.show.open();
    },
  },
};
```

## API

### 声明

| 名称                  | 类型           | 默认值              | 说明                                                         | 必传 |
| --------------------- | -------------- | ------------------- | ------------------------------------------------------------ | ---- |
| ref                   | Boolean        | false               | 通过`ref`调用`open()`和`close()`控制弹出层的打开和关闭       | N    |
| title                 | String         | -                   | 顶部标题                                                     | N    |
| close-btn             | Boolean / Slot | -                   | 是否显示关闭按钮                                             | N    |
| type                  | String         | bottom              | 浮层出现位置。可选项：top/left/right/bottom/center           | N    |
| is-mask-click         | Boolean        | true                | 点击遮罩层是否关闭                                           | N    |
| background-color      | String         | #fff                | 主窗口背景色                                                 |      |
| mask-background-color | String         | rgba(0, 0, 0, 0.55) | 蒙版颜色                                                     |      |
| safeArea              | Boolean        | true                | 是否适配底部安全区                                           |      |
| radius                | String         | -                   | 设置圆角(左上、右上、右下和左下)，如：radius="16px 16px 0 0" |      |

### 插槽

| 名称      | 描述         |
| --------- | ------------ |
| default   | 内容区域     |
| content   | 内容区域     |
| title     | 标题区域     |
| close-btn | 关闭按钮区域 |

### 方法

| 名称  | 参数                                         | 描述       |
| ----- | -------------------------------------------- | ---------- |
| open  | open(String:type) ，如果参数可代替 type 属性 | 打开弹出层 |
| close | -                                            | 关闭弹出层 |

### 事件

| 名称        | 描述                 | **返回值**                            |
| ----------- | -------------------- | ------------------------------------- |
| @change     | 组件状态发生变化触发 | e={show: true ｜ false,type:当前模式} |
| @mask-click | 点击遮罩层触发       | -                                     |

### 外部样式类

| 类名                 | 说明 |
| -------------------- | ---- |
| custom-class         |      |
| custom-class-title   |      |
| custom-class-content |      |
| custom-class-close   |      |
| custom-class-overlay |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |
