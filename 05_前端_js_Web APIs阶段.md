[TOC]

# Web APIs阶段

> JS基础学习ECMAScript基础语法为后面做铺垫，Web APIs是JS的应用，大量使用JS基础语法做交互效果
>
> 在这个阶段主要学习DOM和BOM，实现页面交互功能，Web APIs是JS所独有的部分，需要使用JS基础内容做基础
>
> Web APIs是浏览器提供的一套操作浏览器功能的页面元素的API（BOM和DOM）



**DOM**

- 文档对象模型，处理可扩展标记语言（HTML和XML）的标准编程接口
- 通过DOM接口，可以改变网页内容、结构和样式
- DOM树（DOM把以下内容看成是对象）
  - 文档（document）：一个页面就是一个文档
  - 元素（element）：页面中的所有标签都是元素
  - 节点（node）：网页中所有内容都是节点（标签、属性、文本、注释）



## DOM

### 1. 获取元素

**根据id获取**（了解）

- getElementById()

  - 返回的是一个元素对象

    ```javascript
    <body>
        <div id="'time">2023-5-12</div>
    	//script标签放在body里面，页面是从上往下加载的
        <script>
            var timer = document.getElementById('time');
            console.log(timer);	
    		//dir打印返回的的元素对象，更好的查看里面的属性和方法
            console.dir(timer);		//div#time
        </script>
    </body>
    ```



**根据标签名获取**（了解）

- getElementsByTagName()

  - 返回带有指定标签的对象的集合

  - 若想要依次打印里面的元素对象，可以采取遍历的形式

  - 获取某父元素中的标签类元素：`document.getElementsByTagName('子元素[index]')`

  - 获取父元素中指定标签名的子元素：`element.getElementsByTagName('子元素')`

    ```javascript
    <body>
        <ul>
            <li>这是一个句子1</li>
            <li>这是一个句子2</li>
            <li>这是一个句子3</li>
            <li>这是一个句子4</li>
            <li>这是一个句子5</li>
        </ul>
        <ol id="ol">
            <li>这是句子1</li>
            <li>这是句子2</li>
            <li>这是句子3</li>
            <li>这是句子4</li>
            <li>这是句子5</li>
        </ol>
        <script>
        	//返回的是获取过来的元素对象的集合，以伪数组的形式存储
            var lis = document.getElementsByTagName('li');
            console.log(lis[0]);
    
            varol = document.getElementsByTagName('ol');
            console.log(ol.getElementsByTagName('li'));
    
    		var ol = document.getElementById('ol');
            console.log(ol.getElementsByTagName('li'));
        </script>
    </body>
    ```

    

**根据类名获取**（了解）

- getElementsByClassName('类名')
  - html5新增方法



**指定选择器获取**（重点）

- querySelector('选择器')

  - 类、id、标签名等都可适用
  - 切记，里面的选择器需要加符号（id加#，类加.）

  - 返回指定选择器的存储cc.   cv  第一个对象

    ```javascript
    <body>
        <div class="box">盒子1</div>
        <div class="box">盒子</div>
        <script>
            var boxs2 = document.querySelector('.box');
            console.log(boxs2);							//<div class="box">盒子1</div>
        </script>
    </body>
    ```

- querySelectorAll('选择器')
  
  - 根据指定选择器返回所有元素对象的集合（数组）
  - 得到的是伪数组，没有push()、pop()方法



**获取body、html标签**

```javascript
<script>
    //获取body
    var bodyEle = document.body;
    console.log(bodyEle);
    //获取html
    var htmlEle = document.documentElement;
    console.log(htmlEle);
</script>
```




### 2. 操作元素

> JS的DOM操作可以改变网页内容、结构和样式，我们可以利用DOM操作元素来改变元素里面的内容、属性等



#### 2.1 改变元素内容（旧）

- element.innerText
  
- 不识别html标签
  
  - 从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉
  
- element.innerHTML
  
  - 识别html标签（使用最多）
  
  - 起始位置到终止位置的全部内容，包括html标签，同时保留空格和换行

```javascript
<body>
    <button>显示当前系统时间</button>
    <div>某个时间</div>
    <script>
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        btn.onclick = function() {
            div.innerText = getDate();
        }
		//获得当前时间函数
        function getDate() {
            var date = new Date();
            var year = date.getFullYear();
            var month = date.getMonth() + 1;
            var dates = date.getDate();
            var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            var day = date.getDay();
            return '今天是' + year + '年' + month + '月' + dates + '号 星期' + day;
        }
    </script>
</body>
```



#### 2.1 更改元素内容（新）

- 对象.innerText 属性
  - 显示纯文本，不解析标签

- 对象.innerHTML 属性
  - 解析标签

```javascript
<body>
    <div class="box">我是文字的内容</div>
    <script>
        //修改文字内容innerText
        const box = document.querySelector('.box')
        console.log(box.innerText) //获取文字内容
        box.innerText = '修改过后' //修改文字内容
        box.innerText = '<strong>修改过后</strong>' //不解析标签

        console.log('------------------');
        //修改文字内容innerHTML
        console.log(box.innerHTML) //获取文字内容
        box.innerHTML = '修改过后' //修改文字内容
        box.innerHTML = '<strong>修改过后</strong>' //解析标签
    </script>
</body>
```



#### 2.2 修改元素常见属性

- 可以通过JS设置/修改标签元素属性，比如src更换图片
- 常见属性：herf、title、src等
- 语法：对象.属性 = 值

```javascript
<body>
    <img src="../pic/imag01.jpg" alt="">
    <script>
        //随机数函数
        function randomNum(n, m) {
            return Math.floor(Math.random() * (m - n + 1)) + n;
        }
        // 更改照片路径
        const img = document.querySelector('img')
        img.src = `../pic/image0${randomNum(1,4)}.jpg`
    </script>
</body>
```



#### 2.3 修改样式属性

**通过style修改样式**

- 语法：对象.style.样式属性 = '值'
- 记得跟单位！！！px！！

```javascript
<body>
    <div class="box"></div>
    <script>
		// 修改样式（style）
        const box = document.querySelector('.box')
        box.style.width = '300px'
		box.style.backgroundColor = 'hotpink'  //不能用- 只能用小驼峰命名法
        box.style.borderTop = '2px solid black'
    </script>
```



**通过类名修改样式**

- 若修改的样式比较多，直接通过style修改比较繁琐，可以采用类名修改
- 可覆盖，新值换旧值
- 语法：元素.className = 'active'（active是一个css类名）

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            height: 200px;
            width: 200px;
            background: pink;
        }
    </style>
</head>

<body>
    <p></p>
    <script>
		//修改样式（类名）
        const p = document.querySelector('p')
        p.className = 'box'
    </script>
</body>

</html>
```



**通过classList修改样式（常用）**

- classList追加或删除类名
- 语法：
  - 追加一个类：元素.classList.add('类名')
  - 删除一个类：元素.classList.remove('类名')
  - 切换一个类：元素.classList.toggle('类名')

- 注意：类名不加. 并且还是字符串
- 切换指：有就删掉，没有就加上

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            height: 200px;
            width: 200px;
            background: pink;
        }
        
        .active {
            color: red;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="box">333</div>
    <script>
        //classList修改样式
        const box = document.querySelector('.box')
        box.classList.add('active')
        box.classList.remove('box')
        box.classList.toggle('box')  //有就删掉，没有就加上
    </script>
</body>

</html>
```



#### 2.4 操作表单元素 属性

- 获取：DOM对象.属性名
- 设置：DOM对象.属性名 = 新值
- innerHTML得不到表单
- 表单属性中添加就有效果，移除就没效果，一律使用布尔值表示，如果true代表添加了该属性，false代表移除了该属性
- 例如：disabled、checked、selected

```javascript
<body>
    <!-- <input type="text" value="电脑"> -->
    <input type="checkbox" name="" id="">
    <button>点击</button>
    <script>
        // 获取元素
        const uname = document.querySelector('input')
        // 设置值
        uname.value = 'woyaomai'
        uname.type = 'password'

        const ipt = document.querySelector('input')
        console.log(ipt.checked);
        ipt.checked = true //勾选

        //获取button
        const btn = document.querySelector('button')
        console.log(btn.disabled)
        btn.disabled = true
    </script>
</body>
```



#### 2.5 自定义属性

> 以上为标准属性，比如class、id、title等，可以直接使用点语法操作，比如：disabled、checked、selected

- 自定义属性：
  - html5推出专门的data-自定义属性
  - 标签义data-开头
  - 在DOM对象以dataset对象方式获取

```javascript
<body>
    <!-- 自定义属性 -->
    <div data-id="1" data-spm="buzhidao">1</div>

    <script>
        // 自定义属性
        const div = document.querySelector('div')
        console.log(div.dataset.spm)        //buzhidao
    </script>
</body>
```



### 3.间歇函数（定时器）

> 目标：能够使用定时器函数重复执行代码，定时器函数可以开启和关闭定时器



**开启定时器**

- 作用：每个一段间隔时间，就调用一次这个函数
- 间隔时间是毫秒（1s = 1000ms）

```javascript
//开启定时器
setInterval(函数名,间隔时间)
//关闭定时器
let 变量名 = setInterval(函数,间隔时间)
clearInterval(变量名)
```



```javascript
<body>
    <script>
        // 第一种方式(开启)
        setInterval(function() {
            console.log('1s执行一次');
        }, 1000)

        // 第二种方式(开启)
        function fn() {
            console.log('( •̀ ω •́ )y')
        }

        // 关闭定时器
        let num = setInterval(fn, 1000)
        console.log(num)
        clearInterval(num)
    </script>
</body>
```



### 4. 事件监听

> JS是我们有能力创建动态页面，而事件是可以被JS侦测到的行为，也就是触发相应的一种机制

- 语法：

```javascript
元素对象.addEventListener('事件类型',要执行的函数)
```



**事件三要素**

- 事件源
  - 事件被触发的对象
- 事件类型
  - 如何触发，什么时间；比如鼠标点击（onclick）还是鼠标经过（onmouseover）还是键盘按下
- 事件处理程序
  - 通过一个函数赋值的方式完成

```javascript
<body>
    <!-- 点击按钮就弹出对话框 -->
    <button class="btn">按钮</button>

    <script>
        const btn = document.querySelector('.btn')
        btn.addEventListener('click', function() {
            alert('点击了')
        })
    </script>
</body>
```



**执行事件的步骤**

- 添加事件源
- 注册事件（绑定事件）
- 添加事件处理程序（采取函数赋值形式）



**常见鼠标事件**

| 鼠标事件   | 触发条件         |
| ---------- | ---------------- |
| click      | 鼠标点击左键触发 |
| mouseenter | 鼠标经过触发     |
| mouseleave | 鼠标离开触发     |
| focus      | 获得鼠标焦点触发 |
| blur       | 失去鼠标焦点触发 |
| Keydown    | 键盘按下触发     |
| Keyup      | 键盘抬起触发     |
| input      | 用户输入事件触发 |



#### 4.1 事件对象

- 是什么
  - 也是个对象，这个对象里有事件触发时的相关信息
  - 例如：鼠标点击事件中，事件对象就存了鼠标点在哪个位置等信息
- 使用场景
  - 可以判断用户按下哪个键，比如按下回车键就可以发布新闻
  - 可以判断鼠标点击了哪个元素，从而做出相应的操作



> 也就是  `btn.addEventListener('click', function(e) {}) ` 中的e就是事件对象

```javascript
<input type="text">
<script>
    const input = document.querySelector('input')
    input.addEventListener('keyup', function(e) {
        if (e.key === 'Enter') {
            console.log('按下了Enter键')
        }
    })
</script>
```

##### 4.1.4 trim字符串处理（补）

- 去除字符串左右两端空格，中间空格不去除

```javascript
<script>
    // 去除字符串左右两端空格
    const str = '   i am pink       '    //打印：i am pink
    console.log(str.trim())
</script>
```



#### 4.2 环境对象this

- 指内部特殊的特殊变量this，它代表着当前函数运行时所处的环境
- 普通函数里面，this指的是window
- 谁调用函数，谁就是this



#### 4.3 回调函数

- 如果将函数A作为参数传递给函数B时，我们称函数A为<span style="color:red;">回调函数</span>

```javascript
//fn是回调函数
function fn() {
    console.log('我是回调函数...')
}
setInterval(fn, 1000)
```



#### 4.4 事件解绑

- addEventListener方式，若想解绑，必须使用`removeEventListener(事件类型,事件处理函数[,获取捕获或冒泡阶段])`

*[]代表不是必须参数，可不写*





### 5. 事件流

> 事件流 指 时间完整执行过程中的流动路径，分为捕获阶段和冒泡阶段

- 事件捕获：
  - 从DOM的根元素开始去执行对应的事件（从外到里）
  - 事件捕获需要写对应代码才能看到效果
- 事件冒泡：
  - 当一个元素出发事件后，会依次向上调用所有父级元素的同名事件（比如说都是点击click事件）
  - 事件冒泡是默认存在的
  - L2事件监听第三个参数是false，或者默认都是冒泡

- 阻止冒泡：

  - 需求：想把事件就限制在当前元素内，就需要阻止事件冒泡
  - 前提：阻止事件冒泡需要拿到事件对象
  - 语法：`事件对象.stopPropagation()`

  ```javascript
  <body>
      <div class="fa">
          <div class="son"></div>
      </div>
  
      <script>
          const fa = document.querySelector('.fa')
          const son = document.querySelector('.son')
  
          document.addEventListener('click', function() {
              alert('我是爷爷')
          })
          fa.addEventListener('click', function() {
              alert('我是爸爸')
          })
          son.addEventListener('click', function(e) {
              alert('我是儿子')
                  // 阻止流动
              e.stopPropagation()
          })
      </script>
  </body>
  ```

  

### 6.事件委托

- 优点：减少注册次数，可以提高程序性能
- 原理：利用事件冒泡的特点
  - 给父元素注册事件，当我们触发子元素时，会冒泡到父元素身上，从而触发父元素的事件
- 实现：`事件对象.target.tagName`可以获得真正触发事件的元素















