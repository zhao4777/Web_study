# 前端

## 1. 定位（position）

> 定位（position）是一个更加高级的布局手段，通过定位，可以将元素摆放到页面的任意位置，使用`position`属性来设置定位



`position`

- 可选值：
  - `static`  默认值，元素是静止的没有开启定位
  - `relative`  开启元素的相对定位
  - `absolute`  开启元素的绝对定位
  - `fixed`  开启元素的固定定位
  - `sticky`  开启元素的粘滞定位



### 1.1 相对定位（relative）

> 当元素的position属性值设置为relative时，则开启了元素的相对定位



相对定位的特点：

- 元素开启相对定位以后，如果不设置偏移量元素不会发生任何变化
- 相对定位是参照于元素在文档流中的位置进行定位的
- 相对定位会提升元素的层级
- 相对定位不会使元素脱离文档流
- 相对定位不会改变元素性质，块还是块，行内还是行内



偏移量（`offset`）：

- 当元素开启了定位以后，可以通过偏移量设置元素位置

- top
  - 定位元素和定位位置上边的距离（越大越向下移动）
- bottom
  - 定位元素和定位位置下边的距离（越大越向上移动）
- left
  - 定位元素和定位位置左边的距离（越大越向右移动）
- right
  - 定位元素和定位位置右边的距离（越大越向左移动）

*定位元素垂直方向的位置由`top`和`bottom`两个属性来控制，通常情况下我们只会使用其一（水平方向同理）*

```css
.box2{
    width: 200px;
    height: 200px;
    background-color: orange;
    position:relative;   /*开启定位*/
    top:-200px;          /*先向上移动*/
    left: 200px;         /*再向右移动*/
}
```



### 1.2 绝对定位（absolute）

> 当元素的position属性值设置为absolute时，则开启了元素的绝对定位



绝对定位特点：

- 开启绝对定位后，如果不设置偏移量元素的位置不会发生变化
- 开启绝对定位后，元素会从文档流中脱离
- 绝对定位会改变元素性质，块变行内，块的宽高被内容撑开
- 绝对定位会使元素提升一个层级
- 绝对定位元素是相对于其**包含块**进行决定的



包含块（containing block）：

- 正常情况下
  - 包含块就是里当前元素最近的祖先**块**元素

- 绝对定位的包含块
  - 包含块就是**离它最近**的、**开启了定位**的祖先块元素
  - 如果所有祖先元素都没开启定位，则根元素（html，称初始包含块）就是它的包含块



### 1.3 固定定位（fixed）

> 当元素的position属性值设置为fixed时，则开启了元素的固定定位，固定定位也是一种绝对定位，大部分特点与绝对定位一样



固定定位与绝对定位的不同：

- 固定定位永远参照于浏览器的**视口**（可视窗口，与html不同，html是网页）进行定位
- 固定定位的元素不会随网页的滚动条滚动



### 1.4 粘滞定位（sticky）

> 当元素的position属性值设置为sticky时，则开启了元素的粘滞定位，粘滞定位与相对定位基本一致，兼容性差，**只做了解**



粘滞定位与相对定位的不同：

- 粘滞定位可以在元素到达某个位置时将其固定

```css
.nav{
    width:1210px;
    height: 48px;
    background-color: #E8E7E3;
    margin:100px auto;
    /* 粘滞定位 */
    position: sticky;
    top: 1px;
}
```



### 1.5 绝对定位元素的位置

> **包含块的内容区宽度 = **
>
> **left + margin-left + border-left + padding-left + width + padding-right + border-right + margin-right + right**
>
> **含块的高度 = **
>
> **top + margin-top/bottom + padding-top/bottom  + border-top/bottom + height**





当开启了绝对定位后，水平方向的布局等式就需要添加 left 和 right 两个值，此时规则与之前一样

- 过度约束（9值加在一起不满足等式）时，如果九值中没有 auto ，则自动调整`right`值以使等式满足
- 如果有auto，则自动调整auto的值以使等式满足
  - 可以设auto的值：
    - margin、width、left、right

- 因为 left 和 right 的默认值是auto，所以如果不知道 left 和 right ，则等式不满足时，会自动调整这两个值

  ```css
  .box2{
      width: 100px;
      height: 100px;
      background-color: orange;
      /* 开启绝对定位 */
      position:absolute;
      /*水平居中一定要设置right和left*/
      margin: 0 auto;
      right:0;
      left:0;
  }
  ```

- **包含块的高度 = top + margin-top/bottom + padding-top/bottom  + border-top/bottom + height**

  ```css
  .box2{
      width: 100px;
      height: 100px;
      background-color: orange;
      /* 开启绝对定位 */
      position:absolute;
      /*垂直居中一定要设置right和left*/
      top:0;
      bottom:0;
      margin-top:auto;
      margin-bottom: auto;
  }
  ```

- 如果想要在正中心（既水平居中又垂直居中）

  ```css
  .box2{
      width: 100px;
      height: 100px;
      background-color: orange;
      /* 开启绝对定位 */
      position:absolute;
      margin: 0 auto;
      right:0;
      left:0;
      top:0;
      bottom:0;
      margin-top:auto;
      margin-bottom: auto;
  }
  ```

  

### 1.6 元素的层级

对于开启定位的元素，可以通过`z-index`属性来指定元素层级，`z-index`需要一个整数作为参数

- 值越大，元素的层级越高，层级越高，越优先显示
- 如果元素层级一样，则优先显示靠下的元素
- 祖先元素层级再高，也无法盖住后代元素



## 2. 字体族

`font-size`

- 和font-size相关单位
  - em 相当于当前元素的一个font-size
  - rem 相当于根元素的一个font-size



`font-family`

- 字体样式（格式）
- 指定字体的类别，浏览器会自动使用该类别下的字体
- 可选值
  - serif  衬线字体
  - sans-serif  非衬线字体
  - monospace  等宽字体
- 可以同时指定多个字体，多个字体间使用`,`隔开，字体生效时优先使用第一个，第一个无法使用则会使用第2个

```css
font-family: serif,monospace,sans-serif;
```



### 2.1 图标字体简介（iconfont）

> 在网页中经常需要使用一些图标，可以通过图片来引入图标，但是图片本身比较大，非常不灵活，所以在使用图表示，我们还可以将图标直接设置为字体，然后通过font-face的形式来对字体进行引入，这样就可以直接字体的形式来使用图标



font awesome使用步骤：

- 将css和webfonts移动到项目中
- 将all.css引入到网页中 `<link rel="stylesheet" href="./fa/css/all.css">`
- 使用图标字体
  - 直接通过类名使用图标字体 `  <i class="fas fa-bell"></i>`
    - **其中`fas`是固定的（或者`fab`），后面的`fa-bell`是目标图标的类**











