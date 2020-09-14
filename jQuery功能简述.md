# jQuery 功能简述

## jQuery

jQuery 从 2006 年诞生至今已历经 14 年，仍然是应用最广泛的 JavaScript 函数库。截止 2020 年 7 月，在全世界排名前 100 万的网站中，有超过 80%的网站使用 jQuery。[点击查看统计数据](https://trends.builtwith.com/javascript/jQuery)

## jQuery 的基本功能

jQuery 封装了 DOM 功能，让 DOM 函数的使用变得十分简洁方便。无论是对网页元素的获取还是“增删改查”都进行了更加人性化的封装。下面让我们简单了解一下 jQuery 的基本功能以及 jQuery 设计的优秀之处。

### 一、获取网页元素

#### jQuery 获取的结果是一个对象

- 一些基本方法

```javascript
$(document); // 选择整个文档对象
$("#myId"); // 选择id = 'myId' 的元素
$(".myClass"); // 选择class = 'myClass' 的元素
$("div.myClass"); // 选择class = 'myClass' 的div元素
$("input[name=first]"); // 选择name = 'first' 的 input 元素
```

- jQuery 特有的表达式

```javascript
$("a:first"); // 选择网页中第一个a元素
$("tr:odd"); // 选择表格中的奇数行
$("#myFrom:input"); // 选择表单中的id='myFrom'的input元素
$("div:visible"); // 选择可见的div元素
$("div:gt(2)"); // 选择所有的div元素，除了前3个
$("div:animated"); // 选择当前处于动画状态的div元素
```

- 进一步过滤对 div 的选择结果对象

```javascript
$("div").has("p"); // 选择包含p元素的div元素
$("div").not(".myClass"); //选择class != 'myClass' 的div元素
$("div").filter(".myClass"); // 选择class = 'myClass' 的div元素
$("div").first(); // 选择第1个div元素
$("div").eq(5); // 选择第6个div元素
```

- 通过 div 选择其他元素

```javascript
$("div").next("p"); // 选择div元素后面的第1个p元素
$("div").parent(); // 选择div元素的父元素
$("div").closest("from"); // 选择离div最近的from父元素
$("div").children(); // 选择div的所有子元素
$("div").siblings(); // 选择div同级的其他兄弟元素（不包括自己）
```

### 二、链式操作

#### jQuery 最令人称道的部分

- jQuery 可以对同一对象进行连续函数操作
- 举例：

```javascript
$("div").find("p").addClass("first").removeClass("second").html("third");

// 分解
$("div") // 找到div元素
  .find("p") // 选择其中的p元素
  .addClass("first") // 添加一个class = 'first'
  .removeClass("second") // 删除一个class = 'second'
  .text("third"); // 将文本改为 third
```

- 链式操作是 jQuery 最方便的特点，因为 jQuery 每次执行一个函数操作的返回值还是原来操作的 jQuery 对象，所以可以直接在后面继续操作。

#### .end() 方法

- .end() 方法，使返回值结果退到上一个 jQuery 对象
- 举例：

```javascript
$("div") // 找到div元素
  .find("p") // 选择其中的p元素
  .addClass("first")
  .removeClass("second")
  .text("third")
  .end() // 将jQuery对象从p退回到div
  .addClass("myDiv"); // 给div添加一个class = 'myDiv'
```

### 三、增删改查

#### 1. 增

- 创建新元素：直接在 jQuery 直接传入符合 html 格式的字符串

```javascript
let $myDiv = $("<div class='myDiv'><p>Derek</p></div>"); // 创建新的元素，用变量$myDiv储存
$("body").append($myDiv); // 把$myDiv储存的新元素插入到body中

$("ul").append("<li>list</li>"); // 把新创建的li插入到ul中
```

- 复制元素
  - .clone()
  - 返回当前 jQuery 对象的一个克隆副本
  - 包括所有匹配元素、匹配元素的下级元素、文字节点
  - 2 个参数：
    1. withDataAndEvents 是否同时复制元素的**数据和绑定事件**，默认 false
    2. deepWithDataAndEvents 是否同时复制元素所有子元素的数据和绑定事件，默认值为第 1 个参数(withDataAndEvents)的值

#### 2. 删

- 删除元素
  - .remove() 不保留被删元素的事件
  - .detach() 保留被删元素的事件，便于在重新插入文档时使用
  - .empty() 清空元素内容，但不删除该元素（即删除元素里面的所有节点）

#### 3. 改

- 插入/移动元素

```javascript
$("div").insertAfter($("p")); // 把div元素移动到p元素的后面
$("p").after($("div")); // 把p元素移动到div元素的前面
```

- 上述两种方法的效果是一样的
- 但是它们的返回值是不同的，分别是$('div')和$('p')，所以需要根据后续的操作来进行选择

- 另外两种插入/移动元素的方法

```javascript
// 在div内部的 末端 插入内容
$("div").append("插入的部分");
$("插入的部分").appendTo("div");

// 在div内部的 顶端 插入内容
$("div").prepend("插入的部分");
$("插入的部分").prependTo("div");
```

#### 4. 改查合一 getter/setter

- 同一函数，通过**传参的不同**来实现改/查功能

```javascript
$("h1").html(); // html没有传参，实现取出h1的值
$("h1").html("Hello"); // html传参'Hello'，实现对h1进行赋值
```

- jQuery 常见取值/赋值函数

  - .html() 查/改 html 内容
  - .text() 查/改 text 内容
  - .attr() 查/改 某个属性的值
  - .width() 查/改 某个元素宽度
  - .heigth() 查/改 某个元素高度
  - .val() 查/改 某个表单元素的值

- 注意：
  - 如果结果对象包含多个元素，那么赋值时，将对其中所有的元素赋值
  - 取值时，则是只取出第一个元素的值
  - .text()例外，它取出所有元素的 text 内容
