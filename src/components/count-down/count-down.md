### 使用方法

```vue
<template>
  <count-down
    :time="60000"
    format="HH:mm:ss"
    :auto-start="true"
    :millisecond="false"
    size="medium"
    custom-class="custom-class"
    custom-class-text="custom-class-text"
    @change="handleChange"
    @finish="handleFinish"
  />
</template>

<script>
export default {
  methods: {
    handleChange(timeData) {
      console.log('倒计时变化:', timeData);
    },
    handleFinish() {
      console.log('倒计时结束');
    }
  }
};
</script>
```



### 属性

| 属性名      | 类型             | 默认值     | 说明                               |
| ----------- | ---------------- | ---------- | ---------------------------------- |
| time        | `String, Number` | `0`        | 倒计时时长，单位毫秒               |
| format      | `String`         | `HH:mm:ss` | 时间格式，支持 DD, HH, mm, ss, SSS |
| autoStart   | `Boolean`        | `true`     | 是否自动开始倒计时                 |
| millisecond | `Boolean`        | `false`    | 是否展示毫秒倒计时                 |
| size        | `String`         | `medium`   | 倒计时组件的大小                   |

### 事件

| 事件名  | 说明             | 回调参数                                                     |
| ------- | ---------------- | ------------------------------------------------------------ |
| @change | 倒计时变化时触发 | [timeData](vscode-file://vscode-app/Applications/Visual Studio Code.app/Contents/Resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 对象 |
| @finish | 倒计时结束时触发 | 无                                                           |

### 方法

##### `start()`

开始倒计时。

##### `pause()`

暂停倒计时。

##### `reset()`

重置倒计时。

### 插槽

| 插槽名 | 说明             |
| ------ | ---------------- |
| 默认   | 自定义倒计时内容 |

### 外部样式类

| 类名              | 说明               |
| ----------------- | ------------------ |
| custom-class      | 倒计时组件的样式类 |
| custom-class-text | 倒计时文本的样式类 |