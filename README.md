# 重构代码规范
##一、命名规则
###使用类选择器，杜绝使用ID选择器定义样式
ID在一个页面中的唯一性导致了如果以ID为选择器来写CSS，就无法重用。

###以字母开头
* 必须以字母开头命名选择器，这样可保证在所有浏览器下都能兼容。
* 不允许单个字母的类选择器出现
* 不允许命名带有广告等英文的单词，例如ad,adv,adver,advertising，已防止该模块被浏览器当成垃圾广告过滤掉。任何文件的命名均如此。

###全小写，并使用 ' - ' 连字符
* 下划线 ' _ ' 禁止出现在class命名中，统一使用'-'连字符
* 禁止驼峰式命名
```css
  /* Bad CSS */
  .mod_index{ ... }
  .modIndex{ ... }
  
  /* Good CSS */
  .mod-index{ ... }
```

###命名应简约而不失语义
* 避免过度简写，.ico足够表示这是一个图标，而.i不代表任何意思
* 使用有意义的名称，使用结构化或者作用目标相关的，而不是抽象的名称

###统一语义理解和命名
* aaa

##二、代码格式
###使用4个空格做为缩进
保证在各种环境下显示一致

###每条声明应该只占用一行来保证错误报告更加准确
在一个声明块中只包含一条声明的情况下，为了易读性和快速编辑可以考虑移除其中的换行。所有包含多条声明的声明块应该分为多行。
```css
  /* Bad CSS */
  .selector{padding: 15px; margin: 0px 0px 15px; }
  
  /* Good CSS */
  .selector{
     padding: 15px;     
     margin: 0px 0px 15px; 
  }
```

###使用组合选择器时，保持每个独立的选择器占用一行
```css
/* Bad CSS */
.selector,.selector-a,.selector-b{padding: 15px; margin: 0px 0px 15px; }

/* Good CSS */
.selector,
.selector-a,
.selector-b{    
  padding: 15px;     
  margin: 0px 0px 15px; 
}
```

###所有声明应该以分号结尾
通常在大括号结束前的值可以省略分号，但是这样做会对修改、添加和维护工作带来不必要的失误和麻烦。

###逗号分隔的取值，都应该在逗号之后增加一个空格
比如说box-shadow
```css
/* Bad CSS  */
box-shadow: 0 1px 2px #ccc,inset 0 1px 0 #fff;

/* Good CSS  */
box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
```

###注释格式：/* 注释文字 */
* 对选择器的注释统一写在被注释对象的上一行，对属性及值的注释写于分号后。
* 注释内容两端需空格，已确保即使在编码错误的情况下也可以正确解析样式。
* 在必要的情况下，可以使用块状注释，块状注释保持统一的缩进对齐。
* 原则上每个系列的样式都需要有一个注释，言简意赅的表明名称、用途、注意事项等。
```css
/* 块状注释文字 
 * 块状注释文字 
 * 块状注释文字 
 */
 .m-list{ width : 500px ;}
 .m-list li{     
   height : 20px ;    
   line-height : 20px ;  /* 这里是对line-height的一个注释 */    
   overflow : hidden ;
 }
 .m-list li a{ color : #333 ;}
 /* 单行注释文字 */
 .m-list li em{ color : #666 ;}
```

#三、css语法
###根据属性的重要性按顺序书写 
相关的属性声明应该以下面的顺序分组处理： 

1. Positioning

2. Box model 盒模型

3. Typographic 排版

4. Visual 外观

###坚持限制属性取值简写的使用，属性简写需要你必须显式设置所有取值
* 缩写值可以减少CSS文件大小，并增加可读性和可维护性。
* 但大多数情况下，我们并不需要设置属性简写中包含的所有值。例如，HTML 头部只设置上下的 margin，所以如果需要，只设置这两个值。过度使用属性简写往往会导致更混乱的代码，其中包含不必要的重写和意想不到的副作用。
```css
/* 比如我们用下面这个样式来让某个定宽的容器水平居中，我们要的只是left和right， 
 * 而top和bottom不是这个样式要关心的（如果设置了反倒会影响其他样式在这个容器上的使用），
 * 所以这时我们就不需要缩写 
 */
.f-mgha{    
  margin-left : auto ;   
  margin-right : auto ;
}
/* 比如下面这个模块的样式设置，我们确实需要设置padding的所有项，于是我们就可以采用缩写 */
.m-link{ padding : 6px 12px ;}
```

###不要为 0 指明单位
比如使用 margin: 0; 而不是 margin: 0px;。

###使用单引号
省略url引用中的引号，其他需要引号的地方使用单引号。
```css
.m-box{ background : url (bg.png);}
.m-box:after{ content : '.' ;}
```

###使用16进制表示颜色值,并使用小写字母以及尽量缩写
```css
.m-box{    
  color : #f00 ;     
  background :rgba(0,0,0,.5);
}
```

###不要带有取值前面不必要的 0
比如，使用 .5 替代 0.5，可以减少字节数。

###私有在前，标准在后
先写带有浏览器私有标志的，后写W3C标准的。
```css
.m-box{    
  -webkit-box-shadow :0 0 0 #000 ;    
  -moz-box-shadow :0 0 0 #000 ;   
  box-shadow :0 0 0 #000 ;
}
```

###选择器顺序

请综合考虑以下顺序依据：

* 从大到小（以选择器的范围为准）
* 从低到高（以等级上的高低为准）
* 从先到后（以结构上的先后为准）
* 从父到子（以结构上的嵌套为准）
```css
/* 从大到小 */
.m-list p{    
  margin : 0;     
  padding : 0; 
}
.m-list p.part{     
  margin : 1px ;     
  padding : 1px ;
}
/* 从低到高 */
.m-logo a{ color : #f00 ;}
.m-logo a:hover{ color : #fff ;}

/* 从先到后 */
.g-hd{ height : 60px ;}
.g-bd{ height : 60px ;}
.g-ft{ height : 60px ;}

/* 从父到子 */
.m-list{ width : 300px ;}
.m-list .itm{ float : left ;}
```

###不要以没有语义的标签作为选择器
这会造成大面积污染，除非你可以断定现在或将来你的这个选择器不会污染其他同类
```css
/* Bad CSS */
.m-xxx div{ ... }
```

###不要将选择器写的过于冗长
这会额外增加文件大小并且限制了太小范围的选择器，使树形结构过于严格应用范围过于局限，建议3-4个长度之内写完。
```css
/* Bad CSS */
.m-xxx .class .class .class .class{}
```

###不要越级控制
如果.zzz是.m-yyy的后代选择器，那么不允许.m-yyy之外的选择器控制或修改.zzz。

此时可以使用.m-yyy的扩展来修改.zzz，比如.m-yyy-1 .zzz{}。

###原则上不允许使用Hack
* 很多不兼容问题可以通过改变方法和思路来解决，并非一定需要Hack，根据经验你完全可以绕过某些兼容问题。
* 一种合理的结构和合理的样式，是极少会碰到兼容问题的。
* 由于浏览器自身缺陷，我们无法避开的时候，可以允许使用适当的Hack。

###统一Hack方法
统一使用 “ * ” 和 “ _ ” 分别对IE7和6进行Hack。如下代码所示：
```css
/* IE7会显示灰色#888，IE6会显示白色#fff，其他浏览器显示黑色#000 */
.m-list{    
  color : #000;    
  *color : #888;   
  _color : #fff ;
}
```

###用CSS控制交互或视觉的变化，JS只需要增减className
* 利用CSS一次性更改多个节点样式，避免多次渲染，提高渲染效率。
* 需要在结构中注释此类交互。
