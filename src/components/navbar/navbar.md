## 代码演示

#### 基础演示

```vue
<cy-navbar title="标题文字" />
```

#### 带返回按钮

```vue
<cy-navbar title="标题文字" left-arrow :fixed="false" />
```

#### 自定义

```vue
<cy-navbar :fixed="false">
  <view class="" slot="left">
    left
  </view>
  <view class="" slot="title">
    自定义插槽
  </view>
</cy-navbar>
```

#### 自定义颜色

```vue
<cy-navbar title="标题文字" left-arrow custom-class="custom-navbar" :fixed="false" />
```

```scss
.custom-navbar {
  --cy-navbar-color: #fff;
  --cy-navbar-bg-color: #0052d9;
}
```



## API

### 声明

| 名称       | 类型          | 默认值 | 说明                       | 必传 |
| :--------- | :------------ | :----- | :------------------------- | :--- |
| fixed      | Boolean       | true   | 是否固定在顶部             | N    |
| left-arrow | Boolean       | false  | 是否展示左侧箭头 | N    |
| title      | String / Slot | -      | 页面标题                   | N    |
| visible    | Boolean       | true   | 是否显示                   | N    |
| dark    | Boolean       | true   | 深色导航条                   | N    |
| transparent    | Boolean       | true   | 背景色是否透明                   | N    |
| background    | String       | -   | 自定义背景颜色                   | N    |

### 插槽

| 名称  | 描述         |
| ----- | ------------ |
| left  | 左侧内容区域 |
| title | 标题区域     |

### 事件

| 名称     | 参数    | 描述                                              |
| -------- | ------- | ------------------------------------------------- |
| go-back  | `event` | 点击左侧箭头时触发                                |
| success  | `e`     | navigateBack 执行成功后触发                       |
| fail     | `e`     | navigateBack 执行失败后触发                       |
| complete | `e`     | navigateBack 执行完成后触发（失败或成功均会触发） |

### 外部样式类

| 类名                 | 说明 |
| -------------------- | ---- |
| custom-class         |      |
| custom-class-content |      |
| custom-class-left    |      |
| custom-class-center  |      |
| custom-class-title   |      |

### CSS 变量

组件提供了下列 CSS 变量，可用于自定义样式。

| 名称 | 默认值 | 描述 |
| ---- | ------ | ---- |
|      |        |      |