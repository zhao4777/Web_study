[TOC]

# 前端

## 1. CSS基础

### 1.1 超链接的伪类

超链接的几种状态：

- 没有访问过的链接
- 访问过链接



链接状态表示设置：

 **其中`link`和`visited`是超链接独有的，`hover`和`active`是通用的**

- `link`

用来表示没访问过的链接（正常的链接）

```css
<style>
    a:link{
        color:red;
    }
</style>
```

- `visited`
  - 由于隐私的原因，visited这个伪类只能修改链接颜色

用来表示访问过的链接

```css
a:visited{
     color:green
}
```

- `hover`

不只用于超链接伪类，用来表示鼠标移入的状态，即鼠标移到链接字体上时，字体的改变

```css
a:hover{
    color:orange;
    font-size: 50px;  
}
```

- `active`

表示鼠标点击状态，即点集的一刹那链接字体的改变

```css
a:active{
    color:blue;
}
```



### 1.2 伪元素选择器

伪元素表示页面中一些特殊的、并不真实存在的元素

**伪元素使用`::`开头**

以下是对于**p元素**的伪元素选择器：

- `::first-letter`

表示第一个字母

```css
<style>
    p::first-letter{
        font-size: 50px;
    }
</style>
```

- `::first-line`

表示第一行

```css
p::first-line{
    /*设置背景颜色*/
    background-color: yellow;
    color:red;
}
```

- `::selection`

表示选中的内容

```css
p::selection{
    background-color:pink;
}
```



以下是对于**div元素**的伪元素选择器，**这两个都需要结合`content`属性来使用**：

>  在将来的开发中，这两个伪元素可以用来为某内容前后加标点符号，并且通过before和after加上的内容在网页中不可被选中

- `::before`

对div内容的前面（开始位置）进行操作

```css
div::before{
    content:'abc';
    color: brown;
}
```

- `::after`

对div内容的后面（结束位置）进行操作

```css
div::after{
    content:'hha';
    color: blue;
}
```



### 1.3 样式的继承

- 当我们为一个元素设置一个样式时，这个样式也会应用在它的后代元素上

- 继承发生在祖先与后代之间的

- 继承的设计是为了开发，利用继承我们可以将一些通用的样式同一设置到共同的祖先元素上，这样只需要设置一次即可让所有元素都具有该样式

- 注意：不是所有样式都会继承（背景相关，布局相关）



### 1.4 选择器权重

>  样式冲突
>
> - 当我们通过不同选择器（class，id等），选中相同元素，并为相同的样式（color，font-size等）设置不同的值（red，20px）
> - 发生样式冲突时，由选择器权重（优先级）决定



选择器权重：

- **内联样式 > id选择器 > 类和伪类选择器 > 元素选择器 > 通配选择器 > 继承的样式**

- 交集选择器优先级大于交集选择器中最高优先级的选择器

- 越具体，优先级越高



如果优先级相同，优先使用靠下的样式

可以在后面加个`!important`，则该样式会获得最高优先级

```css
div{
    color:yellow !important;
}
```



### 1.5 像素和百分比

长度单位：

- 像素
  - 屏幕（显示器）实际上是由一个个小点点构成
  - 不同屏幕大小像素大小不同，像素越小的屏幕越清晰
  - 同样的200px在不同设备下显示效果不同

- 百分比
  - 可以设置属性相对于其父元素属性的百分比
  - 可以使子元素跟随父元素改变

- em
  - em是相对于自身元素的字体大小来计算的
  - 1em = 1font-size
  - em会根据字体大小（font-size）改变而改变

- rem
  - 相对于根元素（html）的字体大小来计算



### 1.6 颜色单位

> 在css中可以用颜色名作颜色单位，但是不方便记忆，所以可以使用RGB、RGBA、HSL、HSLA



RGB

- 通过三种颜色不同的浓度调配不同颜色
- R red G green B blue

- 每一种颜色范围在0 - 255 （0% - 100%）之间
- 语法：`RGB(红色,绿色,蓝色)`
- 十六进制的RGB值
  - 语法`#红色绿色蓝色`
  - 颜色浓度范围：00 - ff（eg：#23A966）
  - 如果三个颜色都两位重复可以简写

```css
<style>
    .box1{
        width:100px;
        height:100px;
        /* 颜色单位 */
        background-color: RGB(100,20,30);
    }
</style>
```



RGBA

- 比RGB多一个不透明度
- 透明度范围为0 - 1（1为完全不透明，0为完全透明）
- 语法：`RGB(红色,绿色,蓝色,透明度)`



HSL

- H 色相（0-360） S 饱和度（0%-100%） L 亮度（0%-100%）





## 2. 布局layout

### 2.1 文档流

> 网页是一个多层的结构，一层摞着一层，通过css可以分别为每一层设置样式，作为用户只能看见最上边的一层，这些层中，最底下的一层叫做文档流，文档流是一个网页的基础，我们所创建的元素，默认都是在文档流中进行排列
>
> 对于我们来说，元素主要有两个状态：在文档流中，不在文档流中（脱离文档流）



元素在文档流中的特点：

- 块元素
  - 块元素会在页面中独占一行（自上向下排列）
  - 默认宽度是父元素的全部（会把父元素撑满）
  - 默认高度会被内容撑开（子元素）

- 行内元素
  - 行内元素不会在页面独占一行，只占自身大小
  - 行内元素在页面中自左向右水平排列，如果一行中不能容纳下所有行内元素，则元素会换到第二行继续自左向右排列
  - 行内元素的默认宽度和高度都是被内容撑开



### 2.2 盒子模型（框模型）

> css见个面中所有元素都设置成一个矩形的盒子，所谓的布局就是将不同的盒子放到不同的位置
>
> 内容区、内边距、边框决定盒子大小，外边距决定盒子位置



盒子的构成：

- 内容区（content）
  - 元素中的所有的子元素和文本内容都在内容区中
  - 内容区大小由height和width两个属性设置
- 内边距（padding）
- 边框（border）
  - 边框属于盒子边缘，边框里面属于盒子内部，出了边框都是盒子的外部
  - 边框的大小会影响整个盒子的大小
  - 设置边框至少需要设置三个样式：
    - 边框的宽度 border-width
      - 默认值为3px
    - 边框的颜色 border-color
    - 边框的样式 border-style
- 外边距（margin）

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
        .box1{
            /* 内容区 */
            width:200px;
            height:200px;
            background-color: #bfa;

            /* 边框（border） */
            border-width: 10px;
            border-color: red;
            border-style: solid; /*solid表示实线*/
        }
    </style>
</head>
<body>
    <div class="box1"></div>
</body>
</html>
```



#### 2.2.1 盒子模型-边框（border）

> border-color、border-style与border-width规则相同如下



**边框**

- border-width：

  - 值的情况

    - 四个值：上、右、下、左（`border-width: 10px 20px 30px 40px;`）

    - 三个值：上、左右、下（`border-width: 10px 20px 30px;`）

    - 两个值：上下、左右（`border-width: 10px 20px;`）

    - 一个值：上下左右（`border-width: 10px;`）

  - 除了border-width，还可以是border-xxx-width

    - xxx可以是top right bottom left

- border-style的值及意义

  - 默认值为none

  - solid 表示实线
  - dotted 表示点状虚线
  - dashed 表示线装虚线
  - double 表示双线

- border简写属性（通过该属性可以同时设置边框所有的相关样式，并且没有顺序要求）
  - 语法：border:width color style（eg：`border:10px orange solid;`）
  - 还可以写成border-xxx，xxx可以为：
    - top bottom left right（eg：`border-top:10px green solid;` ）

```css
/*如果不想要右边的边框*/
.box1{
    border:10px green solid;
    border-right:none;
}
```



#### 2.2.2 盒子模型-内边距（padding）

内容区和边框之间的距离是内边距，**一个盒子的可见框大小由内容区、内边距和边框共同决定**，所以计算盒子大小时，需要将这三个区域加到一起计算



**内边距**

- 内边距的设置会影响盒子的大小
- 背景颜色会延伸到内边距上
- 有四个方向的内边距 padding-xxx
  - xxx为top right bttom left
- padding简写属性，可同时指定四个方向的内边距
  - 四值顺序：上、右、下、左（eg：`padding:10px 20px 30px 40px`）
  - 三值顺序：上、左右、下
  - 二值顺序：上下、左右
  - 一值顺序：上下左右

```css
/*head内*/
<style>
    .box1{
        width:200px;
        height:200px;
        background-color: #bfa;
        border:10px orange solid;
        padding-top:100px;
    }
    .inner{
        width:100%;
        height:100%;
        background-color: yellow;
    }
</style>

<body>
    <div class="box1">
		/*inner是box1的内容区，即填满inner即可展现内容区与内边距的面积区别*/
        <div class="inner"></div>
    </div>
</body>
```



#### 2.2.3 盒子模型-外边距（margin）

外边距不会影响盒子可见框大小，会影响盒子的位置



**外边距**

- 四方向外边距（margin-top、bottom、left、right）

  - margin-top
    - 设置一个正值，元素向下移动

  - margin-left
    - 设置一个正值，元素向右移动
  - margin-bottom
    - 设置一个正值，其下边元素向下移动
  - margin-right
    - 默认情况下设置right不会产生任何效果
  - 设置一个负值，会向相反方向移动

- margin简写属性
  - `margin(10px 20px 30px 40px)`，同样有四值、三值、二值、一值，与上同理



### 2.3 盒子模型-水平方向的布局

> 元素在其父元素中水平方向的位置有以下几个属性共同决定：
>
> - margin-left、border-left、padding-left
> - width
> - padding-right、border-right、margin-right



**一个元素在其父元素中，水平布局必须满足以下等式：**

**margin-left + border-left + padding-left + width + padding-right + border-right + margin-right = 其父元素内容区的宽度**

如果根据已确定值（不确定值默认为0）的相加结果不满足上等式，则称为过度约束，则等式会自动调整：

- 七值中有三值可以设置为auto（magin-left、margin-right、width，eg：`width:auto;`）

- 调整情况：

  - 0auto：如果这七个值里没有为auto的情况，则浏览器会自动调整margin-right值以使等式满足

  - 1auto：如果某个值为auto，则会自动调整为auto的值以使等式成立

  - 2auto：如果一个宽度和一个外边距设置为auto，则宽度会调整到最大，设置为auto的外边距会自动为0

  - 2auto：如果将两个外边距设置为auto，width为固定值，则会将两外边距设为相同的值

    - 经常利用这个特点来使一个元素在其父元素水平居中

      ```css
      width:200px;
      margin:0 auto;
      /*两值：上下、左右*/
      ```

  - 3auto：如果三个值都设置为auto，则外边距都是0，宽度最大

  **总结：设置了width为auto，则其他设置为auto的会变为0**



### 2.4 盒子模型-垂直方向的布局

>  默认情况下，父元素的高度被内容撑开
>
> 子元素是在父元素的内容区排列的，如果子元素的大小超过了父元素，则子元素会从父元素中溢出



使用`overflow`属性来设置父元素如何处理溢出的子元素

- 可选值：
  - visible 默认值，子元素从父元素溢出，在父元素外部的位置显示
  - hidden 溢出的内容将会被剪裁不会显示
  - scroll 生成两个滚动条，通过滚动条查看完整内容
  - auto 根据需要生成滚动条

- 除此之外还有overflow-x、overflow-y

#### 2.4.1 外边距折叠

> **相邻**的**垂直**方向外边距会发生重叠现象



相邻的元素的关系：

- 兄弟元素
  - 当两者都是正值或都是负值时，兄弟元素之间的相邻垂直外边距会取两者之间绝对值较大的（取绝对值较大的）
  - 当一正一负时，取两者的和

兄弟元素之间的重叠是对开发有利的，不需要进行处理



- 父子元素
  - 父子元素间的相邻外边距，子元素的会传递给父元素（上外边距）

父子外边距影响页面布局，必须进行处理



### 2.5 行内元素的盒模型

- 行内元素不支持设置width和height

- 行内元素可以设置padding、border、margin，但垂直方向的padding、borderr、margin不会影响页面的布局



将行内元素变为块元素——用属性`display`

`display`用来设置元素显示的**类型**

- 可选值：

  - inline 将元素设置为行内元素

  - block 将元素设置为块元素

  - inline-block 行内块元素

    - 即可以设置width和height，又不会独占一行

  - table 将元素设置为一个表格

  - none 元素不在页面中显示

    ```css
    /*style内*/
    a{
        /* 属性display */
        background-color: orange;
        width:100px;
        height:100px;
         display: block;
    }
    /*body内*/
    <a href="javascript:;">超链接</a>   /*a本来是行内元素，block变为块元素，使width和height属性生效*/
    ```

    

`visibility`用来设置元素的显示**状态**

- 可选值
  - visible 默认值，元素在页面中正常显示
  - hidden 元素在页面中隐藏
    - 与display的none的区别是，hidden依然保留原来块所占的位置，none不保存



### 2.6 浏览器的默认样式

> 通常情况下，浏览器都会为元素设置一些默认样式，默认样式的存在会影响页面的布局
>
> 通常情况下，编写网页时，必须要去除浏览器的默认样式（PC端网页）



*通过网页页面-->右键点击检查-->点击左上角鼠标-->可查看个元素盒子模型的属性值*



**最推荐——引入重置样式表清除**

- link引入的文件一定要在style标签上面！！
- 文件
  - reset .css 直接去除了浏览器的默认样式
  - normalize.css 对默认样式进行了统一

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
	/*方法三，引入reset文件清除*/
    /*<link rel="stylesheet" href="./css/reset.css">*/
	<link rel="stylesheet" href="./css/normalize.css">

    <style>
        .box1{
            width:100px;
            height:100px;
            border:1px solid black;
        }

		/*方法一，一个个标签清除*/
        /* p{
            margin:0px;
        }
        body{
            margin:0;
        }
        ul{
            margin:0;
            margin-left:20px;
            padding:0;
            /*去除项目符号 * /
            list-style: none;
        }  */
        
        /* 方法二，通配选择器清除 */
        /* *{
            margin:0;
            padding:0;
        } */
    </style>
</head>
<body>
    <div class="box1"></div>
    <p>我是一个段落</p>
    <ul>
        <li>列表项1</li>
        <li>列表项2</li>
        <li>列表项3</li>
    </ul>
</body>
</html>
```



### 2.7 盒子大小

> 默认情况下，盒子可见框大小=内容区 + 内边距 + 边框



属性`box-sizing`

- 可选值
  - content-box 默认值，width和height用来设置内容区的大小
  - border-box width和height用来设置整个盒子可见框大小
    - 即width和height指的是内容区和内边距和边框的总大小



### 2.8 轮廓阴影和圆角

#### 2.8.1 轮廓

`outline`用来设置元素的轮廓线，用法和border一样

- 轮廓`outline`和边框`border`的区别是，轮廓不会影响可见框大小，**轮廓不会影响页面布局**



#### 2.8.2 阴影

`box-shadow`用来设置元素的阴影效果，**阴影不会影响页面布局**

- 可选值：
  - 水平偏移量，设置阴影水平位置，正值向右移动，负值向左移动
  - 垂直偏移量，设置阴影垂直位置，正下负上
  - 模糊半径
  - 颜色
  - eg：`box-shadow:20px 20px 20px rgba(0,0,0,.3);`

<img src="E:\前端\笔记截图\屏幕截图 2023-03-30 204518.png" alt="阴影效果图" style="zoom:50%;" />



#### 2.8.3 圆角

`border-radius`用来设置圆角，圆角设置的值是圆的半径大小

- 还可以细分：
  - `border-top-left-radius`
  - `border-top-right-radius`
  - `border-bottom-left-radius`
  - `border-bottom-right-radius`

- 可选值
  - 一值就是圆的半径
  - 两值是椭圆的半径，左上和右下、右上和左下，第一值是水平半径，第二值是垂直半径
  - 三个值 左上、右下和左下、右下
  - 四个值 左上、右上、右下、左下



## 3. 浮动（float）

### 3.1 浮动的简介

>  通过浮动可以使一个元素向它的父元素的左侧或右侧移动



使用`float`属性来设置元素的浮动

- 可选值
  - none 默认值，元素不移动
  - left 元素向左移动
  - right 元素向右移动

**元素设置浮动以后，水平布局的等式偏不需要强制成立**

**元素设置完浮动以后，会完全从文档流中脱离出来，不在占用文档流的位置，所以文档下面的还在文档流中的元素会自动向上移**



浮动特点：

- 浮动元素会完全脱离文档流，不再占用文档流中的位置
- 设置浮动以后，元素会向父元素的左侧或右侧移动
- 浮动元素默认不会从父元素中移出
- 浮动元素向左或向右移动时，不会超过它前面的其他浮动元素
- 如果浮动元素的上面是一个没有浮动的块元素，则浮动元素无法上移
- 浮动元素不会超点他上边的浮动的兄弟元素，最多最多就是和他一样高



### 3.2 浮动的特点

特点：

- 浮动元素不会盖住文字，文字会自动环绕在浮动元素的周围
  - 可以利用浮动设置文字环绕图片的效果
- 元素设置浮动后，将会从文档流中脱离，元素的一些特点也会发生改变
  - 脱离文档流特点：
    - 块元素：
      - 块元素不在独占页面的一行
      - 脱离文档流以后，块元素的宽度和高度都默认被内容撑开
    - 行内元素：
      - 行内元素脱离文档流以后会变成块元素，特点和块元素一样
    - 脱离文档流以后不再需要区分块和行内





### 3.3 简单布局

> 可以简单的将页面看成上（header）、中（main）、下（footer）三个部分，再在三个部分细分



```html
<body>
    <!-- 创建网页头部 -->
    <header></header>

    <!-- 创建网页主体 -->
    <main>
        <!-- 左侧导航 -->
        <nav></nav>

        <!-- 中间内容 -->
        <article></article>

        <!-- 右边栏 -->
        <aside></aside>
    </main>

    <!-- 网页的底部 -->
    <footer></footer>
</body>
</html>
```

效果图：
![效果图](E:\前端\笔记截图\简单布局.png)

### 3.4 高度塌陷和BFC

> 高度塌陷问题：在浮动布局中，父元素默认被子元素撑开，当子元素浮动后，其会完全脱离文档流，子元素从文档流中脱离将会无法撑起父元素的高度，导致父元素的高度丢失，父元素丢失以后，其下的元素会自动上移，导致页面布局混乱
>
> 高度塌陷问题是布局中比较常见的问题，用**BFS**（块级格式化环境）来进行处理



- BFC：是CSS中一个隐含属性，可以为一个元素开启BFC，开启后，该元素会变成一个独立的布局区域

- 元素开启BFC后的特点：
  1. 开启BFC的元素不会被浮动元素覆盖
  2. 开启BFC的元素子元素和父元素外边距不会重叠
  3. 开启BFC的元素可以包含浮动的子元素
- 可以通过一些特殊方式来开启BFC
  1. 设置元素浮动
  2. 将元素设置为行内块元素
  3. 将元素的overflow值设为一个**非visible**的值，用auto或hidden（推荐）





### 3.5 clear

> 如果不希望某个个元素因为其他元素浮动的影响而改变位置，可以通过**clear属性**来清除浮动元素对当前元素产生的影响



clear：

- 可选值
  - left 清除左侧浮动元素对当前元素的影响
  - right 清除右侧浮动元素对当前元素的影响
  - both 清除两侧中较大的那侧
- 原理
  - 设置清除浮动以后，浏览器会自动为元素添加一个上外边距，以使其位置不受其他元素的影响

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1{
            border:10px red solid;

        }
        .box2{
            width: 100px;
            height: 100px;
            background-color: #bfa;
            float:left;
        }
        .box3{
            clear:left;
        }
    </style>
</head>
<body>
    <div class="box1">
        <div class="box2"></div>
        <div class="box3"><!-- aa --></div>
    </div>
</body>
</html>
```

利用after伪类解决高度塌陷

```html
<!--head内-->
<style>
    .box1::after{
        content:'';
        clear:both;         /*取消浮动元素的影响*/
        display: block;    /*将行内元素转换为块元素*/
    }
</style>
<!--body内-->
<body>
    <div class="box1">
        <div class="box2"></div>
        
    </div>
</body>
</html>
```



#### 3.5.1 clearfix

`clearfix`可以同时解决高度塌陷和外边距重叠问题，遇到问题直接使用`clearfix`这个类即可

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1{
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }
        .box2{
            width: 100px;
            height: 100px;
            background-color: orange;
            margin-top: 100px;
        }
        .clearfix::before,
        .clearfix::after{
            content:'';
            /* tabel解决塌陷与外边距重叠 */
            display:table;
            clear:both;
        }
    </style>
</head>
<body>
    <div class="box1  clearfix">
        <div class="box2"></div>
    </div>
</body>
</html>
```



