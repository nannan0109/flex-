[TOC]
# flex笔记——参考阮一峰的博客<br/>
## 0.参考链接
[阮一峰的网络日志——flex布局语法篇][1]
[阮一峰的网络日志——flex布局实例篇][2]
[1]:http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool
[2]:http://www.ruanyifeng.com/blog/2015/07/flex-examples.html
## 1.什么元素可以使用flex?
任何一个容器都可以指定为flex布局
行内元素也可以使用flex布局
webkit内核的浏览器，必须加上-webkit前缀
ps:设置为flex布局后，子元素的float,clear,vertical-align属性将会失效。
## 2.flex容器与项目
采用flex布局的元素，称为flex容器(flex container)，它的所有子元素自动成为容器成员,称为flex项目(flex item)。
容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴(corss axis)。
主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。
项目默认沿着主轴排列。单个项目占据的主轴空间叫做main size,占据的交叉轴空间叫做cross size。<br/>
## 3.容器的6个属性：
* flex-direction
* flex-wrap
* flex-flow
* justify_content
* align-items
* align-content
### 3.1 flex-direction
决定主轴的方向（项目的排列方向）
```
.box{
	flex-direction:row	→
}
.box{
	flex-direction:row-reverse	←
}
.box{
	flex-direction:column	↓
}
.box{
	flex-direction:column-reverse	↑
}
```
### 3.2 flex-wrap
默认情况下，项目都排在一条线上，flex-wrap属性定义，如果一条轴线排不下，如何换行。
默认不换行：
`
.box{
	flex-wrap:nowrap
}
`
换行，第一行在上方：
`
.box{
	flex-wrap:wrap
}
`
换行，第一行在下方：
`
.box{
	flex-wrap:wrap-reverse
}
`
### 3.3 flex-flow
是flex-direction属性和flex-wrap属性的简写方式，默认值为row nowrap
`
.box{
	flex-flow:row || nowrap
}
`
### 3.4 justify-content
定义了项目在主轴上的对齐方式
左对齐：
`
.box{
	justify-content:flex-start
}
`
右对齐：
`
.box{
	justify-content:flex-end
}
`
居中：
`
.box{
	justify-content:center
}
`
两端对齐：项目之间的间隙都相等：
`
.box{
	justify-content:space-between
}
`
每个项目两侧的间隔相等。项目之间的间隔比项目与边框的间隔大一倍。
`
.box{
	justify-content:space-around
}
`
### 3.5 align-items
定义在交叉轴（竖轴）上如何对齐
起点对齐：都从上往下走
`
.box{
	align-items:flex-start
}
`
终点对齐：从下往上走
`
.box{
	align-items:flex-end
}
`
中点对齐：都居中
`
.box{
	align-items:center
}
`
项目的第一行文字的基线对齐：
`
.box{
	align-items:baseline
}
`
默认值，占满整个容器的高度：
`
.box{
	align-items:stretch
}
`
### 3.6 align-content
定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
与交叉轴的起点对齐：
`
.box{
	align-content:flex-start
}
`
与交叉轴的终点对齐：
`
.box{
	align-content:flex-end
}
`
与交叉轴的中点对齐：
`
.box{
	align-content:center
}
`
与交叉轴两端对齐，轴线之间的间隔平均分布：
`
.box{
	align-content:space-between
}
`
每根轴线两侧的间隔都相等：
`
.box{
	align-content:space-around
}
`
轴线占满整个交叉轴（默认值）：
`
.box{
	align-content:stretch
}
`
## 4 项目的6个属性：
* order
* flex-grow
* flex-shrink
* flex-basis
* flex
* align-self
### 4.1 order
定义项目的排列顺序，数值越小，排列越靠前，默认为0（可以为负值）
`
.item{
	order:0
}
`
### 4.2 flex-grow
定义项目的放大比例，默认为0，如果存在剩余空间，也不放大
`
.item{
	flex-grow:1
}
`
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间，如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
### 4.3 flex-shrink
定义了项目的缩小比例，默认为1，如果空间不足，该项目将缩小。
`
.item{
	flex-shrink:1
}
`
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。
如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。
### 4.4 flex-basis
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。
浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
`
.item{
	flex-basis:350px|auto
}
`
### 4.5 flex
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
### 4.6 align-self
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。
默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
`
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
`
该属性可能取6个值，除了auto，其他都与align-items属性完全一致。
***
## 5.基本网格布局
最简单的网格布局，就是平均分布。在容器里面平均分配空间。跟骰子布局很像，但是需要设置项目的自动缩放。<br/>
## 6.百分比布局
某个网格的宽度为固定的百分比，其余网格平均分配剩余的空间。
## 7.圣杯布局
圣杯布局是一种最常见的网站布局。页面从上倒下，分为三个部分，头部（header），躯干（body）,尾部（footer）。
其中躯干分为三栏：从左到右为：导航、主栏、副栏。
## 8.输入框布局
在输入框前方添加提示，后方添加按钮
## 9.悬挂式布局
有时，主栏的左侧或右侧，需要添加一个图片栏
## 10.固定的底栏
有时，页面内容太少，无法占满一屏，底栏就会跑到中间。可以采用flex布局，让底栏总是出现在页面的底部。
## 11.流式布局
每行的项目数固定，会自定分行
