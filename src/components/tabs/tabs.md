

## 代码演示

#### 基础选项卡

```vue
<cy-tabs>
  <cy-tab-panel title="选项1" value="0" />
  <cy-tab-panel title="选项2" value="1" />
</cy-tabs>
```

#### 带底部边框的选项卡

```vue
<cy-tabs bordered>
  <cy-tab-panel title="选项1" value="0">
    <view class="content">0</view>
  </cy-tab-panel>
  <cy-tab-panel title="选项2" value="1">
    <view class="content">1</view>
  </cy-tab-panel>
  <cy-tab-panel title="上限六个文字" value="2">
    <view class="content">2</view>
  </cy-tab-panel>
</cy-tabs>
```

#### 收缩选项卡

```vue
<cy-tabs shrink>
  <cy-tab-panel v-for="i in 8" :key="i" :title="'选项' + i" value="i" />
</cy-tabs>
```

#### 带图标的选项卡

```vue
<cy-tabs>
  <cy-tab-panel v-for="i in 4" :key="i" icon="function-line" :title="'选项' + i" value="i" />
</cy-tabs>
```

#### 带徽标的选项卡

```vue
<cy-tabs>
  <cy-tab-panel title="选项1" dot value="0" />
  <cy-tab-panel title="选项2" badge="8" value="1" />
  <cy-tab-panel title="上限六个文字" value="2" />
</cy-tabs>
```

#### 不同主题

```vue
<cy-tabs type="text">
  <cy-tab-panel title="选项1" value="0" />
  <cy-tab-panel title="选项2" value="1" />
  <cy-tab-panel title="选项3" value="2" />
</cy-tabs>
<cy-tabs type="card">
  <cy-tab-panel title="选项1" value="0" />
  <cy-tab-panel title="选项2" value="1" />
  <cy-tab-panel title="选项3" value="2" />
</cy-tabs>
<cy-tabs type="button">
  <cy-tab-panel title="选项1" value="0" />
  <cy-tab-panel title="选项2" value="1" />
  <cy-tab-panel title="选项3" value="2" />
</cy-tabs>
<cy-tabs type="line-button">
  <cy-tab-panel title="选项1" value="0" />
  <cy-tab-panel title="选项2" value="1" />
  <cy-tab-panel title="选项3" value="2" />
</cy-tabs>
```

#### 竖排选项卡

```vue
<cy-tabs direction="vertical" :animated="false">
  <cy-tab-panel title="选项1" value="0">
    <view class="content">1</view>
  </cy-tab-panel>
  <cy-tab-panel title="选项2" value="1">
    <view class="content">2</view>
  </cy-tab-panel>
  <cy-tab-panel title="选项3" value="2">
    <view class="content">3</view>
  </cy-tab-panel>
</cy-tabs>
```

```scss
.content {
	padding: 16px;
	background: #fff;
}
```

#### 与`Swiper`联动示例

-   请注意`Swiper`组件的`@transition`、`@animationfinish`的支持平台
-   `barAnimateMode="worm"`,设置底部条切换类似毛毛虫蠕动的效果

```vue
<template>
 <view>
     <cy-tabs ref="tabs" v-model="activeIndex" barAnimateMode="worm">
        <cy-tab v-for="(item, index) in tabs" :title="item.title" :key="index" />
     </cy-tabs>
     <swiper class="swiper" :current="activeIndex" @transition="onTransition" @animationfinish="onAnimationfinish" @change="swpierChange">
        <swiper-item v-for="(item, index) in tabs" :key="index">
            <view class="swiper-item-view" :style="{backgroundColor: item.color}">
                {{item.title}}
            </view>
        </swiper-item>
     </swiper>
 </view>
</template>
<script>
    export default {
        data() {
            return {
                tabs: [],
                activeIndex: 0,
            }
        },
        created() {
            this.tabs = Array.from({ length: 5 }, (o, i) => {
                return {
                    title: 'tab' + (i + 1),
                    color: this._getRandomColor()
                }
            });
        },
        methods: {
            //swiper滑动中
            onTransition(e) {
                this.$refs.tabs.setDx(e.detail.dx);
            },
            //swiper滑动结束
            onAnimationfinish(e) {
                this.activeIndex = e.detail.current;
                setTimeout(() => this.$refs.tabs.unlockDx(), 0)  //通知cy-tabs解除对setDx()的锁定
            },
            swpierChange(e) {
                //  由于字节跳动、飞书不支持@animationfinish，因此在change事件中unlockDx
                // #ifdef MP-TOUTIAO || MP-LARK
                this.onAnimationfinish(e)
                // #endif
            },
            // 生成随机颜色
            _getRandomColor() {
                const rgb = [];
                for (let i = 0; i < 3; ++i) {
                    let color = Math.floor(Math.random() * 256).toString(16)
                    color = color.length == 1 ? '0' + color : color
                    rgb.push(color)
                }
                return '#' + rgb.join('');
            },
        },
    }
</script>
<style scoped>
.swiper {
    height: 300rpx;
}

.swiper-item-view {
    background-color: #007AFF;
    height: 300rpx;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 50rpx;
}
</style>
```

## 声明

|              参数              |             类型             |                             描述                             |                            默认值                            |                             说明                             |
| :----------------------------: | :--------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|            v-model             |        number、string        |                   绑定当前选中标签的标识符                   |                              0                               |          即 tab 选中项的下标或者 tab 的 name 属性值          |
|              type              |            string            |                         样式风格类型                         |                             line                             |           可选值为 text、card、button、line-button           |
|             color              |            string            |                          标签主题色                          |                           #0022AB                            |                                                              |
|           background           |            string            |                         标签栏背景色                         |                             #fff                             |                                                              |
|       title-active-color       |            string            |                        标题选中态颜色                        |                              -                               |                                                              |
|      title-inactive-color      |            string            |                        标题默认态颜色                        |                              -                               |                                                              |
|           wrap-style           |            object            |           标签栏样式 案例 ：透明导航栏下的滚动吸顶           |                              -                               |                                                              |
|           direction            |            string            |                       标签栏的展示方位                       |                          horizontal                          |                       可选值：vertical                       |
|            duration            |        number、string        |                       动画时间，单位秒                       |                             0.3                              | 仅支持 type 为 line、button、line-button 的滑块移动的动画时间，标签内容切换时的转场动画时间、页面级滚动导航的内容定位动画时间。 |
|             shrink             |           boolean            | 通过 shrink 属性可以开启收缩布局，开启后，所有的标签会向左侧收缩对齐 |                            false                             |                                                              |
|           bar-width            |        number、string        | 滑块宽度，支持 rpx、vh、vw 等单位及 calc()函数，也可传入'auto'值，默认 px。 | type 为 line，标签栏水平、垂直时宽度分别为 20px、3px，其余为选中标签宽度；为 auto 时，代表滑块宽度自适应于选中标签宽度（仅在 type='line'且 bar-animate-mode='linear'、direction='horizontal'下生效） |          仅支持 type 为 line、button、line-button。          |
|           bar-height           |        number、string        |                 滑块高度，支持度同 bar-width                 | type 为 line，标签栏水平、垂直时宽度分别为 3px、20px，其余为选中标签高度；为 auto 时，代表滑块高度自适应于选中标签高度（仅在 type='line'、bar-animate-mode='linear'、direction='vertical'下生效） |                         同 bar-width                         |
|           bar-style            |            object            |                           滑块样式                           |                              -                               |                         同 bar-width                         |
|        bar-animate-mode        |            string            | 滑动切换 tab 内容时滑块的动画模式，默认为 linear。可选值：worm(毛毛虫蠕动)、worm-ease(毛毛虫缓动效果)、none(不设置)。 |                            linear                            | 仅在 type='line'、direction='horizontal' 时有效。 可结合 swiper 组件使用，效果更好 案例 ：新闻列表、与 swiper 组件联动 |
|           is-dynamic           |           boolean            |                   标签切换后宽高是否有变化                   |                             true                             | 当选中标签会放大文字、减少内间距时，开启该属性可避免滑块错位。（如果选中的标签文字使用‘font-size:20px;transition: all .2s’进行过渡变化，开启该属性仍旧会错位） |
|            ellipsis            |           boolean            |                    是否省略过长的标题文字                    |                             true                             | 标签栏水平展示时，如果标签数量未超过滚动阈值则生效，垂直则不限制。 |
|        scroll-threshold        |        number、string        | 滚动阈值，标签数量超过阈值且总宽度超过标签栏宽度时开始横向滚动 |                              5                               |                                                              |
|        scroll-to-center        |           boolean            |                   标签栏滚动时当前标签居中                   |                             true                             |                                                              |
|         is-lazy-render         |           boolean            |      是否开启延迟渲染（首次切换到标签时才触发内容渲染）      |                            false                             |                                                              |
|            animated            |           boolean            |                         是否开启动画                         |                             true                             | 用于开启标签栏滚动的过渡动画、切换标签内容时的转场动画、滚动导航下的内容定位动画 |
|          active-last           |           boolean            | 在滚动导航模式下，滚动到最后一个标签内容但其顶部未超过可视区域时，是否激活对应的标签项 |                            false                             |                                                              |
|         before-change          | (name) => boolean \| Promise | 切换标签前的回调函数，返回 false 可阻止切换，支持返回 Promise |                              -                               |                   name 为 v-model 绑定的值                   |
|   内容手势滑动切换相关属性 :   |                              |                                                              |                                                              |                                                              |
|           swipeable            |           boolean            | 是否开启手势滑动切换 案例 ：滑动切换 \| 新闻列表 \| 滚动吸顶+左右滑动 |                            false                             |                                                              |
|         swipe-animated         |           boolean            |               是否开启标签内容滑动时的拖动动画               |                             true                             |     swipeable 为 true、且 is-lazy-render 为 false 时有效     |
|        swipe-threshold         |        number、string        | 滑动切换的滑动距离阈值，单位为 px；表示开启手势滑动时，横向滑动多少 px 切换标签内容 |                             120                              |                      快速滑动时不受限制                      |
|       滚动吸顶相关属性 :       |                              |                                                              |                                                              |                                                              |
|             sticky             |           boolean            |         是否使用粘性布局进行滚动吸顶 案例 ：滚动吸顶         |                            false                             |                                                              |
|           offset-top           |        number、string        |         粘性布局下标签栏与顶部的最小距离，单位为 px          |                              0                               |      注意单位问题，如果是 rpx，需要 uni.upx2px 转为 px       |
|            z-index             |        number、string        |               粘性布局下，标签栏的 z-index 值                |                              99                              |                                                              |
|        sticky-threshold        |        number、string        |                    粘性布局吸顶的判断阈值                    |                              0                               | 表示在页面滚动时,标签栏距屏幕顶部多少 px 时会触发吸顶函数进行吸顶判断 案例 ：透明导航栏下的滚动吸顶 |
|          transparent           |           boolean            | 页面滚动过程中,标题栏背景色是否透明渐变 案例 ：透明渐变标题栏 |                            false                             |              background 属性值必须为 rgba 格式               |
|       transparent-offset       |        number、string        |                标题栏背景色透明渐变的滚动距离                |                             150                              |                 请保证标签内容的高度大于该值                 |
| 滚动导航及侧边栏导航相关属性 : |                              |                                                              |                                                              |                                                              |
|           scrollspy            |           boolean            | 是否开启滚动导航；该模式下，内容将会平铺展示 案例 ：滚动导航(页面级滚动) |                            false                             | 如果标签栏垂直展示，且内容平铺展示，就为侧边栏模式案例 ：侧边栏导航(页面级滚动)-仿奶茶点单 |
|          page-scroll           |           boolean            |           滚动导航模式下，内容区域是否跟随页面滚动           |                             true                             | 为 false 时，内容区域是放在 scroll-view 中实现的局部滚动，需自行设置标签页容器高度 案例 ：侧边栏导航(区域滚动)-仿奶茶点单 |

## 事件

|    事件名     |                             说明                             |                           回调参数                           |
| :-----------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|     click     |                        点击标签时触发                        |                  name：标识符，title：标题                   |
|    change     |                   当前激活的标签改变时触发                   |                  name：标识符，title：标题                   |
|   disabled    |                    点击被禁用的标签时触发                    |                  name：标识符，title：标题                   |
|   rendered    |       标签内容首次渲染时触发（仅在开启延迟渲染后触发）       |                  name：标识符，title：标题                   |
| sticky-change |              吸顶时触发，仅在 sticky 模式下生效              |                    { isFixed: 是否吸顶 }                     |
|    loaded     |                   组件内部初始化完成后调用                   |                              -                               |
| slide-change  | 内容页滑动时触发（仅 barAnimateMode 为 linear、worm、worm-ease 时有效） | { dx：滑动距离； rate：当前滑动长度占滑动区域的比例；targetIndex：目标下标；} |
|   slide-end   | 内容页滑动结束时触发（仅 barAnimateMode 为 linear、worm、worm-ease 时有效） |                  { targetIndex: 目标下标 }                   |

## 插槽

|   名称    |                   说明                   |
| :-------: | :--------------------------------------: |
| nav-left  |               标题左侧内容               |
| nav-right |               标题右侧内容               |
|    bar    | 滑块，可自定义滑块的内容(可以设置图片等) |

## 方法

通过 ref 可以获取到 Tabs 实例并调用实例方法(如果是 vue3 的组合式 API,请使用 vue3 的写法)；

|  方法名  |                                                                        说明                                                                         |             参数              | 返回值 |
| :------: | :-------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------: | :----: |
|  resize  |                         外层元素大小、标签数量变化、滑块错位以及标签定位不准时，可以调用此方法来触发组件内部初始化进行调整                          |      callback: 回调函数       |   -    |
|  reset   |                                               重置组件的一些状态，并调用了 resize 方法进行数据初始化                                                |      callback: 回调函数       |   -    |
| scrollTo |                                                      滚动到指定的标签页，在滚动导航模式下可用                                                       |         name: 标识符          |   -    |
|  setDx   | 设置滑块的水平偏移量（结合 swiper 组件的@transition 事件，设置滑块的位置；经过测试，仅在 App、H5、微信、支付宝、字节跳动、QQ 小程序上有良好的效果） | dx: swiper 组件的 e.detail.dx |   -    |
| unlockDx |                              解除对 setDx()的锁定（结合 swiper 组件的@animationfinish 事件，在动画完成后不锁定 setDx）                              |               -               |   -    |

## 注意事项及常见问题

### 组件从隐藏状态切换到显示状态时，底部条位置错误？

Tabs 组件在挂载时，会获取自身的宽度，并计算出底部条的位置。如果组件一开始处于隐藏状态，则获取到的宽度永远为 0，因此无法展示底部条位置。

#### 解决方法

方法一，如果是使用 `v-show` 来控制组件展示的，则替换为 `v-if` 即可解决此问题：

```html
<!-- Before -->
<cy-tabs v-show="show" />
<!-- After -->
<cy-tabs v-if="show" />
```

方法二，调用组件的 resize 方法来主动触发重绘：

```html
<cy-tabs v-show="show" ref="tabs" /> 
```

```js
this.$refs.tabs.resize();
```

### 标签选中后，样式变化可能会导致底部条错误

对于选中的标签，在放大字体的同时添加了过渡样式且有过渡时长，会使标签宽高发生变化，导致内部对于滑块的位置计算错误

#### 解决方法

-   可以考虑给每一个标签通过`title-style`设定固定宽高，避免标签文字放大后标签宽高变化
-   如果没有过渡效果，设置`is-dynamic`即可解决滑块错误的问题，否则有过渡时长使用了该属性也难以保证滑块位置计算正确

### 如何解决上下滑动与左右滑动相冲突？

-   直接给标签内容具体的高度，使用`scroll-view`实现局部滚动 案例 ：滑动切换
-   但是该方式会导致页面级的上拉加载与下拉刷新事件无法触发，因此需要去插件市场找类似的插件

### 切换标签时页面会闪烁？

标签切换后，显示的内容是异步请求获取数据进行渲染的，请给标签内容一个实际的最小高度,避免数据清空后高度回弹有导致页面闪烁

### 在 popup 组件中的 cy-tabs 组件需 resize 一次

对于在`popup`中的`tabs`，在弹出层显示后需调用`resize`方法，避免内部计算错误 案例 ：在 Popup 中的标签页

```html
<cy-popup :visible="show" @close="show = false" @open="open">
	<cy-tabs ref="tabs" v-model="activeIndex">
		...
	</cy-tabs>
</cy-popup>
```

```js
export default{ 
  data(){ 
    return { 
      show: false
    }
  }, 
  methods:{ 
    open(){
			this.show = true; 
      setTimeout(()=> this.$refs.tabs.resize(),1000)
    }
  }
}
```

### 如何在自定义组件中修改 cy-tabs 组件的样式？

在微信小程序端，在自定义组件中使用了`cy-tabs`，需要设置`styleIsolation: 'shared'`,否则在自定义组件中无法修改`cy-tabs`的样式

### 如何修改 cy-tabs 的样式：

-   如果在`自定义组件`或`页面`中引入了 cy-tabs，使用 `::v-deep` 在`cy-tabs`所在的`页面`进行修改

-   将要修改的样式放在全局样式中，但要给`cy-tabs`赋予一个全局唯一的类名，避免全局样式污染

-   仅在微信小程序端，如果自定义组件中使用了`cy-tabs`并想修改其样式，需要在自定义组件上配置`styleIsolation: 'shared'`

    ```javascript
    export default {
    	options: {
    	    styleIsolation: 'shared'
    	},
    }
    ```

### 侧边栏导航、滚动导航模式

-   两者内容区域的滚动方式通过`pageScroll`属性控制
-   为 false 时，则表示内容页是放在`scroll-view`中实现的局部滚动 案例 ：滚动导航(区域滚动) | 侧边栏导航(区域滚动)
-   为 true 时，则表示内容区域是在页面上的，跟随页面滚动而滚动(页面级滚动) 案例 ：滚动导航(页面级滚动) | 侧边栏导航(页面级滚动)
-   如何取舍两者之间的使用，根据场景考虑，比如你的标签页上方有 banner 图，你需要在滚动过程中让标题栏浮动时，则需要页面级滚动,或者需要触发原生的上拉加载、下拉刷新事件也用该方式；
-   如果你想两种模式在一定高度内滚动，那么就使用局部滚动。

### 如果标签栏仍出现滚动条，请在全局样式（可放在 APP.vue 引入的样式文件）中添加如下 css：

```scss
// 隐藏scroll-view的滚动条
::-webkit-scrollbar {
	display: none;
	width: 0 !important;
	height: 0 !important;
	-webkit-appearance: none;
	background: transparent;
}
```

### 如果在进入页面时又跳转了其他页面，会导致 cy-tabs 内部未初始化完成，因此底部条会错位：

-   场景：进入‘我的’页面，检测到用户未登录，跳转至登录页进行登录后又回到‘我的’页面

-   解决方法如下：

    ```js
    export default {
    	onShow() {
    	// 如果进入该页面又跳转了其他页面，则在onShow中resize一下组件，避免跳转其他页面时tabs内部未初始化完成
    	this.$refs?.tabs?.resize()
    	},
    }
    ```
