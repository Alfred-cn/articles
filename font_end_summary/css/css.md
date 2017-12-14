CSS基础
====

盒模型
----  
盒模型：content->padding->border->margin；  
margin不在width的范围内，同理height;  
css3 新增属性box-sizing;

content-box(default):
----

布局所占宽度Width:  
width = width + padding-left + padding-right + border-left + border-right;   

布局所占高度Height:  
height = height + padding-top + padding-bottom + border-top + border-bottom;   

padding-box:
----
布局所占宽度width:
width = width(包含padding-left + padding-right) + border-left + boder-right;

布局所占高度height:  
height = height(包含padding-top + padding-right) + border-top + border-bottom;  

border-box:  
----
布局所占宽度width:  
width = width(包含padding-left + padding-right + border-left + border-right);  

布局所占高度height:  
height = height(包含padding-top + padding-bottom + border-top + border-bottom);  

***********************************************************************************************

CSS文档流
====

css普通文档流：按照HTML中声明的顺序排布。  
float和绝对定位布局不在文档普通流里面。

display属性：
----
常见block属性元素： div, h1-6, ul, li, ol, etc.  
常见inline属性元素：span, a, em;

block:
----
宽度自行设置，默认宽度由父容器决定，默认高度由内容决定，独占一行；

inline: 
----
宽度和高度都由内容决定，与其他元素共占用一行；

inline-block:
----
宽度可以自行设定，类似block，与其他元素共占一行。  

position属性:
====
默认定位属性为static，其实就是未被设置定位。  
如果元素被定位了（也就是positioned了），它的top，left，bottom，right值就会生效，能设置定位的属性是relative，absolute和fixed。  

relative：
----
元素相对定位，是相对于父节点偏移了top,left,bottom和right值，元素会在自身文档流所在的位置上被移动，其他元素则不会调整位置来弥补它偏离后剩下的空隙。

absolute:
----
绝对定位之后，元素脱离文档流，元素偏移是相对于它最近设置了定位属性（position不是static）的元素。  

fixed:
----
基于可视window定位；

css 居中布局：
===

1.完全居中：

```css
//父容器样式
.Center-Container {
  position: relative;
  width: 500px;
  height: 500px;
}

//base： 针对父容器居中
.Absolute-Center {
  width: 60%;
  height: 60%;
  //overflow: auto;
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  text-align: center;
}


```

**********************************************************************************************************************************

css选择器:
===

CSS选择器优化:
----
css基本选择器, css属性选择器, css伪类选择器；
浏览器读取选择器的顺序是由右到左进行。

css选择器固定效率：
----
- id选择器；
- 类选择器；
- 标签选择器；
- 相邻选择器；
- 子选择器；
- 后代选择器；
- 通配符选择器；
- 属性选择器；
- 伪类选择器；

css优先级算法
----
优先级为：   
内联样式表（标签内style形式）-> 嵌入样式表(当前文件中style标枪) -> link标签；   
!important > id > class > tag


CSS Hack Skill
====

单行文本溢出显示省略号:
----
```css
style {  
	overflow: hidden;    
	text-overflow:ellipsis;  
	white-space: nowrap;  
}
```

多行文本溢出显示省略号:
----
	
```css
.detail-font {
    font-size: 0.3rem;
    margin: 0.0rem;
    overflow : hidden;
    /*text-align: justify;*/  //两端对齐,有Bug
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
}
```


	



  







