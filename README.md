# cy-uni-design
诚驿uni小程序组件库



使用vscode打开并npm i，运行项目到小程序可以预览组件样式。

组件在src/components里



### 配置步骤

#### 1. 引入全局SCSS主题文件

在项目src目录的uni.scss中引入此文件。

<!--本组件依赖SCSS，您必须要安装此插件，否则无法正常运行。-->

```
/* uni.scss */
@import '@/cydesign-miniprogram/variables.scss';
```

#### 2. 引入基础样式

> 注意要写在第一行，同时给style标签加入lang=”scss”属性

```
/* App.vue */<style lang="scss">    /* 注意要写在第一行，同时给style标签加入lang="scss"属性 */    @import "@/cydesign-miniprogram/common/index.scss";</style>
```

#### 3. 配置easycom组件模式

此配置需要在项目src目录的pages.json中进行。

> uni-app为了调试性能的原因，修改easycom规则不会实时生效，配置完后，您需要重新编译项目才能正常使用。
> 请确保您的pages.json中只有一个easycom字段，否则请自行合并多个引入规则。

```
// pages.json{
"easycom": {
	"autoscan": true,
		"^cy-(.*)": "@/cydesign-miniprogram/$1/$1.vue"
	}
}
```



## 内置样式

### 边框

```
<!-- 上边框 -->
<view class="cy-hairline--top"></view>
<!-- 下边框 -->
<view class="cy-hairline--bottom"></view>
<!-- 左边框 -->
<view class="cy-hairline--left"></view>
<!-- 右边框 -->
<view class="cy-hairline--right"></view>
<!-- 全边框 -->
<view class="cy-hairline--surround"></view>
```

### 安全区

```
<!-- 顶部安全区 -->
<view class="cy-safe-area-top"></view>
<!-- 底部安全区 -->
<view class="cy-safe-area-bottom"></view>
```

### 文字截断

```
<!-- 超出一行不显示 -->
<view class="cy-ellipsis"></view>

<!-- 超出N行不显示 -->
<view class="cy-ellipsis-2"></view>
<view class="cy-ellipsis-3"></view>
```



## 样式覆盖

### 1. 使用 Style

cyDesign 默认开启 virtualHost 属性

```
<cy-button custom-style="color: red">填充按钮</cy-button>
```

### 2. 解除样式隔离

#### 在页面中使用

cyDesign 全体组件均开启了 addGlobalClass，可以接受外部传入的样式。

```
<cy-button theme="primary">填充按钮<cy-button>
.cy-button--primary {
	background-color: red;
}
```

#### 在自定义组件中使用

> 需要在自定义组件的 options 中开启： styleIsolation: ‘shared’

```
<cy-button theme="primary">填充按钮<cy-button>
```

自定义的组件：

```
Component({
	options: {
		styleIsolation: 'shared'
	}})
	
.cy-button--primary {  
	background-color: red;
}
```

### 3. 使用外部样式类

cyDesign 在每个组件的内部都预置了许多外部样式类供使用。

```
<cy-button custom-class="red-color">填充按钮<cy-button>
.red-color {  
	color: red !important;
}
```

### 4. 使用 CSS 变量

cyDesign 为所有组件预置了许多 CSS 变量，具体可以查看每个组件开发者模式下的元素页面。

```
page {  --cy-button-default-color: red;}
```



## 图标

图标库使用[Remix Icon](https://remixicon.com/)

### 安装

```
npm install remixicon --save

import 'remixicon/fonts/remixicon.css'
```

### 使用

```
// 组件的icon props不需要加「ri-」
<cy-icon name="home-line" size="32" />
<cy-button theme="primary" icon="add-line">添加</cy-button>

// 单独使用需要全名
<view class="ri-add-line">添加</view>
```
