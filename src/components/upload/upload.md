## 代码演示

#### 只选择图片

```vue
<cy-upload v-model="imageValue" limit="9" :source-type="sourceType" />
```

```js
export default {
	data() {
		return {
      imageValue: [],
			sourceType: ['album', 'camera'],
		}
	}
}
```

#### 只选择视频

```vue
<cy-upload v-model="value" limit="9" media-type="video" :source-type="sourceType" />
```

```js
export default {
	data() {
		return {
      value: [],
			sourceType: ['album', 'camera'],
		}
	}
}
```

#### 组件状态

```vue
<cy-upload v-model="status" limit="9" :source-type="sourceType" />
```

```js
export default {
	data() {
		return {
			status: [{
				"name": "loading.jpg",
				"extname": "jpg",
				"url": "",
				"status": 'loading',
				"progress": -1
			}, {
				"name": "progress.jpg",
				"extname": "jpg",
				"url": "",
				"status": 'progress',
				"progress": 68
			}, {
				"name": "error.jpg",
				"extname": "jpg",
				"url": "",
				"status": 'error'
			}],
      sourceType: ['album', 'camera'],
		}
	},
},
```

#### 手动上传

```vue
<view>
  <cy-upload ref="files" :auto-upload="false"/>
  <button @click="upload">上传文件</button>
</view>
```

```js
export default {
		data() {},
		methods:{
			upload(){
				this.$refs.files.upload()
			}
		}
	}
```

#### 自定义来源

```vue
<cy-upload limit="9" title="从相册选图" media-type="image" :source-type="['album']" />

<cy-upload limit="9" title="使用相机" media-type="video" :source-type="['camera']" />
```

#### 组件标题

```vue
<cy-upload title="最多选择9张图片" />
```

#### 自定义上传按钮

```vue
<cy-upload media-type="image">
  <cy-icon name="share-2-line" />
</cy-upload>

<cy-upload media-type="video">
  <cy-button size="small">自定义按钮</cy-button>
</cy-upload>
```



## API

### 声明

| 名称            | 类型          | 默认值                     | 说明                                                         | 必传 |
| --------------- | ------------- | -------------------------- | ------------------------------------------------------------ | ---- |
| v-model/value   | Array/Object  | -                          | 组件数据，通常用来回显 ,类型由`return-type`属性决定，**格式下文** | N    |
| disabled        | Boolean       | false                      | 组件禁用                                                     | N    |
| readonly        | Boolean       | false                      | 组件只读，不可选择，不显示进度，不显示删除按钮               | N    |
| return-type     | String        | array                      | 限制 `value` 格式，当为 `object` 时 ，组件只能单选，且会覆盖 | N    |
| disable-preview | Boolean       | false                      | 禁用图片预览，仅 `mode:grid`生效                             | N    |
| del-icon        | Boolean       | true                       | 是否显示删除按钮                                             | N    |
| auto-upload     | Boolean       | true                       | 是否自动上传，值为`false`则只触发@select，可自行上传         | N    |
| limit           | Number/String | 9                          | 最大选择个数                                                 | N    |
| title           | String        | -                          | 组件标题                                                     | N    |
| mode            | String        | list                       | 选择文件后的文件列表样式，可选`list/grid`                    | N    |
| media-type      | String        | image                      | 选择文件类型，可选`image/video/all`，all 只支持微信小程序    | N    |
| file-extname    | Array/String  | -                          | 选择文件后缀，字符串的情况下需要用逗号分隔（推荐使用字符串），根据 `media-type` 属性而不同 | N    |
| size-type       | Array         | ['original', 'compressed'] | original 原图，compressed 压缩图，默认二者都有               | N    |
| source-type     | Array         | ['album', 'camera']        | album 从相册选图，camera 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项 | N    |

### 插槽

| 名称    | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| default | 默认插槽，根据`media-type`属性不同，自定义的位置也不同。<br />如果`media-type="image"`仅为自定义方框内图标<br />如果`media-type="video"`则为完全自定义 |

### 事件

| 名称     | 参数 | 描述                 |
| :------- | :--- | :------------------- |
| select   | -    | 选择文件后触发       |
| progress | -    | 文件上传时触发       |
| success  | -    | 上传成功触发         |
| fail     | -    | 上传失败触发         |
| delete   | -    | 文件从列表移除时触发 |

### value 格式

| 名称     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| name     | 文件名称                                                     |
| extname  | 文件扩展名                                                   |
| url      | 文件地址                                                     |
| status   | 文件状态，如果为`error`则显示‘重新上传’按钮，值为`done`时为上传完成 |
| progress | 上传进度，值为`-1`时显示'上传中'，`0-100`时显示具体上传百分比 |

### 方法

通过 `$ref` 调用

|         方法称名         |                        说明                         |                        参数                        |
| :----------------------: | :-------------------------------------------------: | :------------------------------------------------: |
|         upload()         | 手动上传 ，如`autoUpload`为`false` ，必须调用此方法 |                         -                          |
| clearFiles(index:Number) |                    清除选择结果                     | 传入 Number　为删除指定下标的文件 ，不传为删除所有 |

### 外部样式类

| 类名         | 说明 |
| ------------ | ---- |
| custom-class |      |

