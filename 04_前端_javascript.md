

[TOC]

# Javascript基础阶段

## 1. 介绍

> 是一种运行在客户端的语言，是脚本语言



描述类语言：

- HTML
  - 决定网页结构和内容（决定看到什么）
- CSS
  - 决定网页呈现给用户的模样（决定好不好看）

脚本语言（逐行解释）：

- JS
  - 实现业务逻辑和页面控制



JS组成：

- ECMAScript：规定了编程语法和基础核心知识
- Web APIs
  - DOM：文档对象模型（页面元素移动、大小、添加删除等）
  - BOM：浏览器对象模型（页面弹窗、检测窗口宽度、存储数据到浏览器等）

（mdn网站可做辅导）

## 2. 基础

### 2.1 书写位置

> 注意js代码用的是**单引号**

**行内**

```html
<body>
    <!-- 1.行内 -->
    <input type="button" value="唐伯虎" onclick="alert('秋香姐')">
</body>
```

**内嵌**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 2.内嵌 -->
    <script>
        alert('沙漠骆驼');
    </script>
</head>

```

**外部**

script标签中间一定不要写代码！！

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 3.外部引入 -->
    <script src="my.js"></script>
</head>

```



### 2.2 输入输出语句

- 输入框 `prompt`

  - prompt取过来的值是字符型的

  ```javascript
  prompt('请输入你要输入的的内容：');
  ```

- 弹出警示框 `alert`

  - 输出的，展示给用户的

  ```javascript
  alert('计算的结果是：');
  ```

- 控制台输出 `console.log`

  - 给程序员测试用的

  ```javascript
  console.log('我是程序员能看到的');
  ```

  

### 2.3 变量

`typeof 变量`  返回变量类型

**2.3.1 声明变量**

用`var`关键字来进行声明，声明变量的同时赋值变量，叫做变量的初始化。

*2023更新：现在利用`let`来声明变量

```javascript
<script>
    var a=prompt('请输入你要输入的内容：'),
        b=18;
    console.log(a);
</script>
```

- 如果只声明不赋值，结果是undefined
- 不声明，直接赋值使用会变成全局变量（不推荐）

**2.3.2 声明常量**

用`const`关键字声明，不允许更改，声明时必须赋值



### 2.4 数据类型

> js的变量数据类型是只有程序在运行过程中，根据等号右边的值来确定的。
>
> js是动态语言，变量的数据类型是可以变化的

共有Number、String、Boolean、Undefined、Null类型

**2.4.1 Number**

- 有浮点型和整型
  - 如果表示八进制，在数字前面加`0`
  - 如果表示十六进制，在数字前面加`0x`
- `Number.MAX_VALUE`  查看数值最大值，同理`Number.MIN_VALUE`  查看数值最小值
- `Infinity`  表示无穷大
- `NaN`  表示一个非数字
  - `isNaN`  用来判断非数字，如果是数字返回`false`



**2.4.2 String**

- 推荐使用**单引号**
- 引号嵌套**（外单内双、外双内单）**
- 转义字符`\`

长度：字符串长度可以用 `length` 属性获取

拼接：多个字符串之间可以用 `+` 继续拼接，其拼接方式为 **字符串 + 任何类型 = 拼接之后的新字符串**

模板字符串：注意：外面包的是反引号，而不是单引号。

```javascript
<script>
        // 模板字符串
        let age = 19;
        document.write(`我今年${age}岁了`);
</script>
```



**2.4.3 Undefined、Null**

- undefined与数字相加结果为NaN、null与数字相加结果为数字
- 与字符串相加，结果就是连起来



**2.4.4 数据类型转换**

- 转为字符串型

  - 变量.toString

    - 转换为字符串

  - String(变量)

    - 强制转换为字符串

  - 加号拼接字符串（重要）

    - 和字符串拼接的结果都是字符串

    ```javascript
    var num=1;
    alert(num+'');
    ```



- 转为数字型

  - parseInt(string)函数（重要）

    - 括号内必须以数字开头

    ```javascript
    parseInt('78');
    parseInt('120pxabc');   //120 会去掉这个px单位
    ```

  - parseFloat(string)函数（重要）

    ```javascript
    parseFloat('79.21');
    ```

  - Number()强制转换函数

    ```javascript
    Number('21')
    ```

  - 隐式转换（-  * /）

    ```java
    '12'-0;
    ```

  

- 转为布尔类型
  - Boolean()函数
    - 代表空的、否定的值会被转换为`false`



### 2.5 运算符

- ==  默认转换数据类型，会把字符串型的数据转换为数字型，只要求**值**相等

  ```javascript
  console.log(18 == '18');   //true
  ```

- === 或 !== 全等，必须**值**与**数据类型**必须完全要一模一样

  ```javascript
  console.log(18 === '18');   //false
  ```


- 三元运算符：条件 ? 满足条件执行的代码 : 不满足条件执行的代码

  ```javascript
  console.log(3>5 ? 3 : 5)
  num = num < 10 ? 0 + num : num    //小于10的补位0
  ```



### 2.6 数组

创建数组的方式：

- 利用new来创建

  ```javascript
  var arr = new Array();
  ```

- 利用字面量创建

  ```javascript
  var arr = [];  //创建一个空数组
  var arr = [1, true, 'yes'];
  ```

- 数组名.length 可访问数组长度



修改数组长度

- 利用 数组名.length 修改数组长度

  ```javascript
  arr.length = 5;
  ```

- 新增数组元素

  ```javascript
  var arr = [2,3,'y'];
  arr[3]='no';    //arr = [2,3,'y','no']
  arr.push(6)     //arr = [2,3,'y','no',6]
  
  ```

  

 ### 2.7 函数

函数的声明：function

- 较为自由

```javascript
/*方法一 具名函数*/
/*可以先声明后使用，也可以先试用后生声明*/
function getMax(arr){
    var max = arr[0];
    for(int i = 1;i<=arr.length; i++){
        if(arr[i] > max){
            max = arr[i];
        }
    }
    return max;
}
var re = getMax([0,5,7,1,4]);
console.log(re);

/*方法二 匿名函数*/
/*只能先声明后使用*/
var fun = function(){
    console.log('2');
}

/*匿名函数：立即执行函数*/
/*前后必须有分号*/
;(function(x,y) {})(1,2);
(function(x,y) {}(1,2));
fun();
```

```javascript
function getResult(num1, numm2){
    return [num1 + num2, num1 - num2];
}
```



伪数组：

- 有length
- 有索引
- 没有真正数组的一些方法（pop()、push()等 ）

当不确定有多少个参数传递的时候，可以用`arguments`来获取，`arguments`存储了所有传递过来的的实参，是个伪数组

```javascript
function fn(){
    console.log(arguments)  //arguments(3)=[1,2,3]
}
fn(1,2,3);
```



注意：

- 在函数内部没有定义，而是直接赋值的变量也是全局变量。



### 2.8 预解析

> js引擎运行js分为两步：预解析 、 代码执行



预解析：

- js引擎会把js里面所有的var和function提升到当前作用域的最前面

- 分为变量预解析（变量提升）和函数预解析（函数提升）
- 变量提升
  - 把所有变量的声明提升到当前的作用域最前面，不提升赋值操作

- 函数提升
  - 把所有函数的声明提升到当前的作用域最前面，不调用函数

```javascript
function f1(){
    var a = b = c = 9;  //相当于var a=9;b=9;c=9; b和c直接赋值，没有var声明，当全局变量看
    console.log(a);
    console.log(b);
    console.log(c);
}
f1();
console.log(c);
console.log(b);
console.log(a);
//99999报错
```



### 2.9 对象

创建对象的方法

- 字面量创建（属性）

  - 花括号 {} 包含对象的属性与方法

  ```javascript
  var obj = {
      uname:'anna',
      'goods-name':'小米'
      age:19,
      sayHI:function(){
          console.log('hi');
      }
  }
  //调用对象属性
  console.log(obj.uname);
  console.log(obj['age']);
  console.log(obj['goods-name']);
  //调用对象方法
  obj.sayHI();
  ```



- new Object创建

  ```javascript
  var obj2 = new Object();
  obj2.uname = 'coco';
  obj2.age = 10;
  obj2.say = function() {
      console.log('h');
  }
  ```

  

- 对象中的方法

  - 在对象外调用：对象名.方法名()
  - 经典例子：document.write()

  ```javascript
  <script>
      let obj = {
              uname: '刘德华',
              // 方法
              song: function() {
                  console.log('冰雨');
              }, //用逗号隔开
              dance: function() {
                  console.log('这是dance')
              }
          }
          // 方法调用：对象名.方法名
      obj.song()
  </script>
  ```

  

- 构造函数创建

  - 可利用函数的方法，重复代码，构造对象，将对象里面一些相同的属性和方法抽象出来封装到函数里面

  ```javascript
  function Star(uname, age, sex) {    //构造函数的函数名要大写
      //属性
      this.name = uname;
      this.age = age;
      this.sex = sex;
      //方法
      this.sing = function(sang) {
          console.log(sang);
      }
  }
  var ldh = new Star('刘德华', 18, '男');
  ldh.sing('一首歌');
  var ldh = new Star('张学友', 19, '男');
  ```

  - new执行时会做的四件事：
    - 在内存中创建一个新的空对象
    - 让this指向这个新的对象
    - 执行构造函数里面的代码，给这个新对象添加属性和方法
    - 返回这个新对象



#### 2.9.1 遍历对象

> 使用for...in语句遍历对象

```javascript
for (var k in ldh) {
    console.log(k); //输出属性名
    console.log(ldh[k]); //输出属性值
}
```



#### 2.9.2 内置对象

> js提供了多个内置对象：Math、Date、Array、String等，利用MDN文档进行查询

##### （1） Math

```javascript
console.log(Math.abs(-1))   	//1，绝对值函数 
console.log(Math.PI)			//3.141592689793
console.log(Math.floor(-3.5))	//-4，向下取整
console.log(Math.ceil(-3.5))	//-3，向上取整
console.log(Math.round(-1.5))	//-1，四舍五入，就近取整（.5往大取）
console.log(Math.max(1,2))		//2,取最大值
```

**随机数方法random()**

- 返回一个随机的小数，取值范围为：0 <= x < 1

- 函数里无参数

- ```javascript
  console.log(Math.random());
  //得到两个数区间的随机整数，包括两个数在内
  function getRandomIntInclusive(min,max){
      //min=Math.ceil(min);
      //max=Math.floor(max);
      //比如：想取0-10之间的数：Math.floor(Math.random()*(10+1))
      return Math.floor(Math.random()*(max-min+1)+min);
  }
  
  //随机点名
  var arr = ['张三', '李四', '王五', '小刘'];
  console.log(arr[getRandomIntInclusive(0, arr.length-1)]);
  ```



##### （2）Date

- Date()日期对象是一个构造函数，必须用new来调用创建日期对象

- 没有参数时，返回当前系统的的时间

- 参数常见写法

  - 数字型：2019,10,01     
  - 字符型：'2019-10-1 8:8:8'

- ```javascript
  var date1 = new Date(2019, 10, 01);
  console.log(date1);        //Fri Nov 01 2019 00:00:00 GMT+0800 (中国标准时间)  注意：输出的为Nov，不是10月
  var date2 = new Date('2019-10-01 8:8:8');
  console.log(date2);			//Tue Oct 01 2019 08:08:08 GMT+0800 (中国标准时间)
  
  var date = new Date();
  console.log(date.getFullYear());  	//2023
  console.log(date.getMonth());		//4，（0-11）
  console.log(date.getDate());		//10
  console.log(date.getDay());			//3（周日为0，周六为6，0-6）
  console.log(date.getHours());		//19
  console.log(date.getMinutes());		//56
  console.log(date.getSeconds());		//43
  ```

- 对于时间小于两位数时，补0问题

  ```javascript
  function getTime() {
      var time = new Date();
      var h = time.getHours();
      //小于两位数补0
      h = h < 10 ? '0' + h : h;
      var m = time.getMinutes();
      m = m < 10 ? '0' + m : m;
      var s s= time.getSeconds();
      s = s < 10 ? '0' + s : s;
      return h + ':' + m + ':' + s;
  }
  console.log(getTime());
  ```

  

##### （3） Array

**检测是否为数组**

- instanceof

  ```javascript
  var arr = [];
  console.log(arr instanceof Array);   //True
  ```

- Array.isArray()

  ```javascript
  console.log(Array.isArray(arr));
  ```

  

**添加元素**

- push()

  - push完毕后返回的结果是新数组的长度，原数组也会发生变化

  - 在数组末尾添加一个或多个数组元素

    ```javascript
    var arr=[1,2,3];
    console.log(arr.push(5,'yes'));		//5
    console.log(arr);					//[1,2,3,5,'yes']
    ```

- unshift()

  - unshift完毕后返回的是新数组的长度，原数组也会发生变化

  - 是在数组的开头添加一个或多个元素

    ```javascript
    console.log(arr.unshift('red',0)); 	 //7
    console.log(arr);          			 //[0,'red',1,2,3,5,'yes']
    ```



**删除元素**

- pop()

  - unshift完毕后返回的是删除的那个元素，原数组也会发生变化

  - 只能删除数组的最后一个元素

    ```javascript
    console.log(arr.pop());			//pink
    console.log(arr)				//[0,'red',1,2,3,5]
    ```

- shift()

  - shift完毕后返回的是删除的那个元素，原数组也会发生变化

  - 只能删除数组的第一个元素

    ```javascript
    console.log(arr.shift());		//0
    console.log(arr)				//['red',1,2,3,5]
    ```

    

**数组排序**

- reverse()

  - 翻转数组

- sort()

  - 缺点：双位数排序有误

    ```javascript
    //改进：
    var arr1=[13,4,77,1,7];
    arr1.sort(function(a,b){
        return a-b;		//升序排列
       //return b-a;	//降序排列
    })
    console.log(arr1);			//[1,4,7,13,77]
    ```

    

**数组索引**

- indexOf()

  - 返回该元素在数组内的索引号，值返回第一个满足条件的索引号

  - 找不到元素返回-1

    ```javascript
    var arr=['red','blue','green','yellow'];
    console.log(arr.indexOf('blue'));		//2
    ```

  - 字符串类型也可用`str.indexOf('要查找的字符',[起始位置]);`

    ```javascript
    var str = '你好我是爱学习的学生';
    console.log(str.indexOf('学'));		//5
    console.log(str.indexOf('学', 7));	//8
    ```

    

- lastindexOf()
  
  - 从后往前查找，返回的索引号还是正向的索引号
  - 找不到元素返回-1



**数组转换为字符串**

- toString()

  ```javascript
  var arr=[1,2,3];
  console.log(arr.toString());
  ```

- join(分隔符)

  ```javascript
  var arr=['green','blue','red'];
  console.log(arr.join('-'));
  ```

  

##### （4） String

**根据位置返回字符**

- charAt(index)
  - 返回指定位置的字符本身
- charCodeAt(index)
  - 返回指定位置的字符的ASCII码
- str[index]
  - 返回指定位置的字符本身



**字符串操作方法**

- concat(str1,str2,...)
  
  - 拼接字符串，用于连接两个或多个字符串
- substr(start,length)
  
  - 从start开始索引，取length个数的字符
- slice(start,end)
  
  - 从start开始，截取到end位置，end取不到
- substring(start,end)
  
- 从start开始，截取到end，end取不到，不接受负值
  
- replace('被替换的字符','替换为的字符')

  - 只替换第一个字符

    ```javascript
    var str1 = 'aaabbbccc';
    console.log(str1.replace('a', 'b'));  //baabbbccc
    ```

- split('分隔符')

  - 将字符转换为数组（join将数组转化为字符）

    ```javascript
    var str2 = 'red,pink,yellow';
    console.log(str2.split(','));		//['red', 'pink', 'yellow']
    ```

    















