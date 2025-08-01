## 代码演示

#### 基础吸顶

```
<view class="title">基础吸顶</view>
<cy-sticky>
    <cy-button>吸顶</cy-button>
</cy-sticky>
```

#### 吸顶距离

```
<view class="title">吸顶距离</view>
<cy-sticky :offset-top="100">
    <cy-button>吸顶距离</cy-button>
</cy-sticky>
```

#### 框内吸顶

```
<view class="title">框内吸顶</view>
<view class="example" style="height: 300px; border: 1px solid #000; margin: 0 40px;">
    <cy-sticky>
        <cy-button>吸顶</cy-button>
    </cy-sticky>
</view>
```


## API

### 声明

| 名称        | 类型                   | 默认值  | 说明                                                         | 必传 |
| :---------- | :--------------------- | :------ | :----------------------------------------------------------- | :--- |
| z-index     | String / Number          | 99      | 层级                                                      | N    |
| offset-top | String / Number | 0       | 吸顶时与顶部的距离，单位`px`                                     | N    |


### 插槽

| 名称    | 描述     |
| :------ | :------- |
| default | 默认插槽 |
