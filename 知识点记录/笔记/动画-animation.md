## 动画-animation

动画是由三部分组成

关键帧 - 定义动画在不同阶段的状态。

动画属性 - 决定动画的播放时长，播放次数，以及用何种函数式去播放动画等。（可以类比音视频播放器）。

css属性 - 就是css元素不同关键帧下的状态

### 关键帧(@keyframes)

语法：@keyframes animationname {keyframes-selector {css-styles;}}

注释：

keyframes-name是帧列表的名称，名称必须符合CSS语法中对标识符的定义。

from
等效于 0%.

to
等效于 100%.

### 动画属性

动画属性可以理解为播放器的相关功能，一个最基本的播放器应该具有：播放/暂停、播放时长、播放顺序(逆序/正序/交替播放)、循环次数等。

简写属性：

```
animation:
animation-name animation-duration // 动画的名称、持续时间
animation-timing-function animation-delay // 关于时间的函数(properties/t)、延迟时间
animation-iteration-count animation-direction // 播放次数、播放顺序
animation-fill-mode animation-play-state// 播放前或停止后设置相应样式、控制动画运行或暂停
```

两个必选属性：
animation-name animation-duration // 动画的名称、持续时间

#### animation-timing-function

定义了动画的播放速度曲线，可以使用数学函数，称为三次贝塞尔曲线，速度曲线。

>ease 默认值。动画以低速开始，然后加快，在结束前变慢.

>ease-in 动画以低速开始.

>ease-out 动画以低速结束.

>ease-in-out 动画以低速开始和结束.

>linear 匀速

>cubic-bezier(number, number, number, number) 贝塞尔曲线.

#### animation-direction

表示CSS动画是否反向播放。

>animation-direction: normal 正序播放

>animation-direction: reverse 倒序播放

>animation-direction: alternate 交替播放

>animation-direction: alternate-reverse 反向交替播放

>animation-direction: normal, reverse

>animation-direction: alternate, reverse, normal

#### animation-delay - 动画延迟

定义动画是从何时开始播放。

#### animation-iteration-count

定义我们的动画播放的次数，默认是1次。（infinite是播放无限次）

#### animation-fill-mode

是指给定动画播放前后应用元素的样式

>animation-fill-mode: none 动画执行前后不改变任何样式

>animation-fill-mode: forwards 保持目标动画最后一帧的样式

>animation-fill-mode: backwards 保持目标动画第一帧的样式

>animation-fill-mode: both 动画将会执行 forwards 和backwards 执行的动作

#### animation-timing-function

定义动画是否运行或者暂停。可以确定查询它来确定动画是否运行。
默认值为running

>running 动画正常播放

>paused 动画暂停播放

## 动画-animation-事件

当你需要在某个动画开始或者结束时,去触发某一个事件,那么这时候可以用到监听animation事件方法。

### -webkit-animation动画其实有三个事件:

animation涉及到的事件有 animationStart、animationEnd、animationIteration三个。

[注意] 对于safari浏览器，animation的事件为webkitAnimationStart、webkitAnimationEnd、webkitAnimationIteration

```
 //开始事件 webkitAnimationStart
 //结束事件 webkitAnimationEnd
 //重复运动事件 webkitAnimationIteration
```

#### animationStart

发生在动画开始时

1、如果存在delay，且delay为正值，则元素等待延迟完毕后，再触发该事件

2、如果delay为负值，则元素先将初始值变为delay的绝对值时，再触发该事件

#### animationEnd

发生在动画结束时

#### animationIteration

发生在动画的一次循环结束时，只有当iteration-count循环次数大于1时，触发该事件

#### 补充

只有改变animation-name时，才会使animation动画效果重新触发。

example：

```
Element.style.animationName = 'none';
setTimeout(function(){
    Element.style.animationName = 'aName';
},100);
```

#### 属性

这三个事件的事件对象，都有animationName和elapsedTime属性这两个私有属性

> animationName属性: 返回产生过渡效果的CSS属性名

> elapsedTime属性: 动画已经运行的秒数