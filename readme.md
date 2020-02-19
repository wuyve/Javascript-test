<!-- TOC -->

- [搭建javascrpt笔试/测试环境](#搭建javascrpt笔试测试环境)
    - [下面的方法介绍如何从0搭建一个可以测试JavaScript代码的环境：](#下面的方法介绍如何从0搭建一个可以测试javascript代码的环境)
    - [本文件如何下载并应用？](#本文件如何下载并应用)
- [下面的方法介绍node.js测试/笔试方法：](#下面的方法介绍nodejs测试笔试方法)
    - [下面是有关输入条件（行数）的技巧/方法：](#下面是有关输入条件行数的技巧方法)
        - [1. 单行输入](#1-单行输入)
        - [2. 多行输入](#2-多行输入)
- [下面是我遇到的一些笔试题：](#下面是我遇到的一些笔试题)

<!-- /TOC -->

### 搭建javascrpt笔试/测试环境
有些前端笔试的编程中，编程语言是没有node.js，只有JavaScript，但是要求获取输入（多行或单行）并且要输出。但是本地vscode或html中没有相关环境可以测试代码/笔试。

如下图所示：
![截图](./static/cut1.png)

#### 下面的方法介绍如何从0搭建一个可以测试JavaScript代码的环境：
1. 新建一个文件夹，在文件夹内，安装cnpm install readline-sync
2. 添加一个index.js文件，文件中输入以下代码：
```javascript
var __readline = require('readline-sync');
__readline.setDefaultOptions({
    prompt: ''
});
var read_line = __readline.prompt;
var print = console.log;
// 这里是要测试的js代码
```
3. 这样子，js带输入输出的本地笔试环境搭建完毕。

[参考文档](https://www.cnblogs.com/yujihang/p/7413906.html)


#### 本文件如何下载并应用？
1. 下载本project到本地
`git clone https://github.com/wuyve/Javascript-test.git`
2. 安装相关依赖包
`npm install`
3. 在`index.js`文件中输入需要测试/调试/笔试的代码，根据需要修改输入输出的变量名
4. 运行index.js
`node index.js`或`node index`


### 下面的方法介绍node.js测试/笔试方法：
搭建环境（本地要安装node）：
1. 新建一个js文件；
2. 输入nodejs代码；(推荐文档[Node.js之readline(按行读取)](http://nodejs.cn/api/readline.html))
3. 运行/测试/调试代码`node [文件名]`或`node [文件名.js]`

#### 下面是有关输入条件（行数）的技巧/方法：
##### 1. 单行输入
```javascript
var readline = require('readline');
var readlineTest = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
readlineTest.on('line', function(line){
    let str = line;  
    // 注意：这里的str不论在shell中输入的是数字还是字符串，获取到的始终是字符串，必要时要将其转换为所需要的数据类型
    console.log(str);

    // 下面是处理数据的函数
    // ...
    // 上面是处理数据的函数

    // 关闭node输入环境
    readlineTest.close();
})
```
##### 2. 多行输入
```javascript
var readline = require('readline');
var readlineTest = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
var lineCounts=3;  // 输入数据为3行
var arr=[]; // 创建数组来存储每一行的数据
var index=0; // 初始化数组的索引
readlineTest.on('line', function(line){
    // 注意：这里的line不论在shell中输入的是数字还是字符串，获取到的始终是字符串，必要时要将其转换为所需要的数据类型
    arr[index]=line;

    // 这里可以处理每一行的数据

    index++;
    if(arr.length==lineCounts){

        // 这里可以处理lineCounts行(全部)的数据

        console.log(arr[i]);
        // 关闭node输入环境
        readlineTest.close();
    }
});
readlineTest.on('close', function() {
    process.exit(0);
});
```

### 下面是我遇到的一些笔试题：
1. 去哪儿编程题1（语言：Node.js， 通过率：86%）

    由于航司规定，对单次搜索的成人和儿童数量有如下限制：
    1. 成人至少选择一个，儿童可不选
    2. 一次最多只能指定9个乘机人
    3. 一个成人最多只能携带2个儿童出行
    
    输入
    
        >输入成人和儿童个数
        
    输出
    
        > 如果成人和儿童数量不符合规则，输出：选择不合法
        
    否则输出：
    
        > 第一行：成人可选择的数量
        
        > 第二行：儿童可选择的数量
例如：

输入

> 1,2

输出

> 1,2,3,4,5,6,7

> 0,1,2

```javascript
var readline = require('readline');
var readlineTest = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
readlineTest.on('line', function(line){
    let str = line;
    while(str.indexOf("，")!=-1)
    {
        str=str.replace("，",",");
    }
    let arr = str.split(',');
    let adultNum = Number(arr[0]), childrenNum = Number(arr[1]);
    if (adultNum === 0) {
        console.log('选择不合法');
    } else if (childrenNum > (adultNum * 2)) {
        console.log('选择不合法');
    } else if ((adultNum + childrenNum) > 9) {
        console.log('选择不合法');
    } else {
        let audltArr = [], childrenArr = [];
        for (let i = 1; i <= 9 - childrenNum; i++) {
            if (i * 2 >= childrenNum && i + childrenNum < 10) {
                audltArr.push(i)
            }
        }
        for (let i = 0; i <= childrenNum; i++) {
            childrenArr.push(i)
        }
        audltArr = audltArr.join(',');
        childrenArr = childrenArr.join(',');
        console.log(audltArr);
        console.log(childrenArr);
    }
    readlineTest.close();
})
```

2. 去哪儿编程题2(语言：Node.js，通过率： AC)

    为了能让用户尽快找到低价机票，我们从服务器渠道航班数据后需要按价格进行排序，然后展示给用户。
    排序规则：
    1. 按照价格从低到高进行排序
    2. 相同价格按照 rank 值同高到低排序
    3. 排序完成后按行输出 name:rank:code:price
    
    输入
    
        > 一行包含航班数据的json字符串
        
    输出
    
        > 按行输出排序后的航班 
        
        > 行模板：name:rank:code:price
        
测试用例：

输入

> {"k3845": {"name": "name3012","price": 2715,"rank": 1},"k3489": {"name": "name2855","price": 3105,"rank": 1},"k845": {"name": "name7788","price": 1111,"rank": 1},"k77889": {"name":"name7746588","price": 1111,"rank": 2}}

输出

> name7746588:2:k77889:1111

> name7788:1:k845:1111

> name3012:1:k3845:2715

> name2855:1:k3489:3105

```javascript
var readline = require('readline');
var readlineTest = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
readlineTest.on('line', function(line){
    let jso = line;
    jso = JSON.parse(jso);
    let arr = [];
    for (let i in jso) {
        let obj = {};
        obj.code = i;
        obj.name = jso[i].name;
        obj.price = jso[i].price;
        obj.rank = jso[i].rank;
        arr.push(obj);
    }
    arr.sort((a,b) => {
        if (a.price !== b.price) {
            return a.price - b.price;
        } else {
            return b.rank - a.rank;
        }
    })
    for (let i = 0; i < arr.length; i++) {
        let result = `${arr[i].name}:${arr[i].rank}:${arr[i].code}:${arr[i].price}`
        console.log(result);
    }
    readlineTest.close();
})
```

3. 腾讯笔试：数组平铺（语言： Node.js； 通过率： 笔试结束后写的，未测试通过率）

测试用例：

输入

> [1,2,[3,4,[5,6,[7,[8,9]]]]]

输出

> [1,2,3,4,5,6,7,8,9]

```javascript
var readline = require('readline');
var rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
})
var arrIn = []
var arrOut = []
rl.on('line', (input) => {
    arrIn = input;
    console.log('arrIn', arrIn);
    console.log(typeof arrIn);
    var pattern = /^[0-9]*$/
    for (var i = 0; i < arrIn.length; i++) {
        console.log(arrIn[i])
        if (arrIn[i].match(pattern)) {
            arrOut.push(~~arrIn[i])
        }
        console.log(arrOut)
    }
    // arrOut = arrIn.split(",").map(item => Number(item));
    console.log('arrOut', arrOut);
    console.log(typeof arrOut);
    rl.close()
})

```

4. 腾讯笔试： 计算出输入的年份中二月有多少天（语言：Node.js； 通过率：AC）

测试用例：

输入：

> 2019

输出：

> 28

```javascript
//  引入readline模块
var readline = require('readline');

//  创建一个readline接口实例
var readlineTest = readline.createInterface({
    
    input: process.stdin,
    output: process.stdout
});
var year = 0;
var days = 0;
readlineTest.on('line', function(line){
    year = line;
    if (year % 4 === 0 && year % 10 !== 0 || year % 400 === 0) {
        console.log('29');
    } else {
        console.log('28');
    }
});
//当readlineTest执行'close'命令时，输入流关闭，程序结束。
readlineTest.on('close', function() {
    process.exit(0);
});
```

1. JS的判断类型
2. ES6扩展了哪些东西
3. Proxy对象能拦截什么
4. Promise 
5. JS实现异步的5种方式callback, 发布订阅模式，Promise，生成器函数，async/await
6. 实现异步的Event Loop，即浏览器端的宏任务，微任务，以及nodejs中的几个事件循环阶段
7. 如果阻塞了JS中的主线程会发生什么情况
8. 发布订阅设计模式，其实这就是一个nodejs中的EventEmitter
9. PureComponent，flex布局以及一些css的东西，比如水平垂直居中
10. 用css实现一个模态窗口，要从窗口下面向上弹的动画
11. css的单位比如rem，em，问css的布局方式
12. 盒子模型布局，position的布局，flex布局，grid布局等
13. 跨域的问题，如何解决，我说了后端响应时设置Access-control-allow-origin头部，还有JSONP，然后他就那个响应头问的比较深
14. XSS攻击
15. CSRF
16. 节流函数
```javascript
function throttle (fn, time) {
    var canRun = true;
    return function () {
        if (!canRun) return false;
        canRun = false;
        var that = this, args = arguments;
        setTimeout(function () {
            fn.apply(that, args);
            canRun = true;
        }, time || 500);
    }
}
setInterval(throttle(function() {
    console.log("hello world")
}), 100)
```
17. reduce实现map的功能
```javascript
Array.prototype.map = function (callback) {
    var arr = this;
    return arr.reduce((acc, cur, i) => {
        acc.push(callback(cur, i, arr));
        return acc
    }, []);
}
var m = [1,2,3,4,54].map(function (v, i, arr) {
    return v * v
});
console.log(m)
```
18. 实现二叉树的后序遍历
```javascript
function TreeNode (val) {
    this.val = val;
    this.left = null;
    this.right = null;
}
 
function vist(root) {
    if (root) {
        vist(root.left);
        vist(root.right);
        console.log(root.val);
    }
}
```
19. 对Vue的理解
20. css2 和css3中垂直居中
css3新增了一些属性，像flex，这是css3中很重要的改变，所以除了flex以外的垂直水平居中的技巧都是属于css2的。
- css2的水平居中技巧
将元素display为行内元素，再text-align:center;即可
或者
将块级元素定义一个宽度，再margin: 0 auto;即可
- css3的水平居中技巧
将元素display设为flex，再通过justify-content: center; 实现居中。
- css2的垂直居中技巧
单行内容的垂直居中可以通过设置相同height值和line-height值来实现。
多行内容的垂直居中且高度可变可以通过设置上下相同的padding值来实现。
行级盒子：小图标和标题对齐设置vertical-align: middle。
绝对定位：top:50%; left:50%;的方法，需要已知块级的宽高
- css3的垂直居中技巧
将元素display设为flex，再通过align-items:center;来实现。
21. 计算机网络的认识
22. 计算机网络的七层
应用层、表示层、会话层、传输层、网络层、数据链路层、物理层
23. TCP和UDP的区别是什么
TCP：面向连接、传输可靠(保证数据正确性,保证数据顺序)、用于传输大量数据(流模式)、速度慢，建立连接需要开销较多(时间，系统资源)
UDP：面向非连接、传输不可靠、用于传输少量数据(数据包模式)、速度快
24. TCP和UDP属于计算机网络中的哪一层
网际层协议：IP协议、ICMP协议、ARP协议、RARP协议
传输层协议：TCP协议、UDP协议
应用层协议：FTP、Telnet、SMTP、HTTP、RIP、NFS、DNS
25. HTTPS是什么
HTTPS即加密的HTTP，HTTPS并不是一个新协议，而是HTTP+SSL（TLS）。原本HTTP先和TCP（假定传输层是TCP协议）直接通信，而加了SSL后，就变成HTTP先和SSL通信，再由SSL和TCP通信，相当于SSL被嵌在了HTTP和TCP之间
26. 介绍几种常见的状态码
2XX系列：代表请求已成功被服务器接收、理解、并接受。
200状态码：表示请求已成功，请求所希望的响应头或数据体将随此响应返回
201状态码：表示请求成功并且服务器创建了新的资源，且其 URI 已经随Location 头信息返回。
3XX系列：代表需要客户端采取进一步的操作才能完成请求，这些状态码用来重定向，后续的请求地址（重定向目标）在本次响应的 Location 域中指明。
301状态码：被请求的资源已永久移动到新位置。服务器返回此响应（对 GET 或 HEAD 请求的响应）时，会自动将请求者转到新位置。
302状态码：请求的资源临时从不同的URI响应请求，但请求者应继续使用原有位置来进行以后的请求。
304状态码：自从上次请求后，请求的网页未修改过。服务器返回此响应时，不会返回网页内容。
4XX系列：表示请求错误。代表了客户端看起来可能发生了错误，妨碍了服务器的处理。
401状态码：请求要求身份验证。 对于需要登录的网页，服务器可能返回此响应。
403状态码：服务器已经理解请求，但是拒绝执行它。与401响应不同的是，身份验证并不能提供任何帮助，而且这个请求也不应该被重复提交。
404状态码：请求失败，请求所希望得到的资源未被在服务器上发现。
5xx系列：代表了服务器在处理请求的过程中有错误或者异常状态发生，也有可能是服务器意识到以当前的软硬件资源无法完成对请求的处理。
500状态码：服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。
503状态码：由于临时的服务器维护或者过载，服务器当前无法处理请求。
27. 闭包是什么
闭包就是能够读取其他函数内部变量的函数。
闭包的用途：可以读取函数内部的变量，并且让这些变量的值始终保持在内存中。
28. NaN是什么，用typeof会输出什么
Not a Number
会输出 Number
29. 跨域问题如何解决
同源策略：浏览器安全策略，同协议、ip、端口的脚本才会执行。
只要协议、域名、端口有任何一个不同，都被当作是不同的域
js跨域是指通过js在不同的域之间进行数据传输或通信
    1. 通过jsonp跨域
    jsonp在页面上引入不同域上的js脚本文件实现请求不同域上的数据
    (1) 通过script标签引入一个js文件
    (2) js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入
    注：需要服务器端的页面进行相应的配合
    2. 通过修改document.domain来跨子域
    3. 使用window.name来进行跨域
    window对象有个name属性，该属性有个特征：即在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。
30. 知道babel么
可以实现将ES6编译为ES5代码
31. 用js实现判断一个变量是否为整数的函数
实现思路：先判断该变量是否为Number类型，以此来缩小范围，再判断该变量除以1后是否与原值全等，若全等则返回true，若不全等则返回false
32. 进程和线程是什么
线程是最小的执行单元，而进程由至少一个线程组成。如何调度进程和线程，完全由操作系统决定，程序自己不能决定什么时候执行，执行多长时间。
进程指计算机中已运行的程序。
线程指操作系统能够进行运算调度的最小单位。
33. 快速排序用js怎么写
function quickSort(arr) {
  if(arr.length<=1) {
  	return arr;
  }
  var s = Math.floor(arr.length/2);
 
  var temp = arr.splice(s,1);
  
  var left=[];
  var right=[];
  for(var i=0;i<arr.length;i++) {
    if(arr[i]<temp) {
      left.push(arr[i]);
    }
    if(arr[i]>=temp) {
      right.push(arr[i]);
    }
  }
  
  return quickSort(left).concat(temp,quickSort(right));  
  
}
34. 函数中的arguments是数组吗？类数组转数组的方法了解一下？
arguments当然不是数组啦，转数组的方法有：
    [...arguments]
    Array.from(arguments)
35. == 是非严格比较操作符，false会转换为0，[]会转换成''，{}会转换为"[object Object]"，
[]和{}是“空”的对象，不是“空”，所以会输出3
最后一个引用地址不一致，不是同一个对象，所以不会输出4
36. 按要求写出一个throttle防抖函数
37. 一个字典['I', 'have', 'a', 'book', 'good']，实现一个函数，判断一个字符串中是否都是出自字典中的，输出true/false
例如：

输入'I have a book' 输出 true

输入 'this is a good book' 输出 false
38. http缓存
39. display的取值和各种值的区别？
40. 相邻的两个inline-block节点为什么会出现间隔，该如何解决？
41. 前端性能优化有哪些？
42. 找出数组中和为给定值的两个元素，如：[1, 2, 3, 4, 5]中找出和为6的两个元素。
冒泡排序
```javascript
function getNum(arr, sum) {
    if (!Array.isArray(arr)) return null;

    for (var i = 0; i < arr.length - 1; i++) {
        if (arr[i] > sum) continue;

        for (var j = 0; j < arr.length; j++) {
            if (arr[j] > sum) continue;

            if (arr[i] + arr[j] == sum) return [arr[i], arr[j]];
        }
    }

    return null;
}
```
查找的方式
function getNum(arr, sum) {
    if (!Array.isArray(arr)) return null;

    arr.sort();

    for (var i = 0; i < arr.length - 1; i++) {
        if (arr[i] > sum) continue;

        var restNum = sum - arr[i];

        // 考虑下为什么要 > i
        if (arr.indexOf(restNum) > i) return [arr[i], restNum];
    }

    return null;
}
```
这种解法的前提是需要对数组进行排序（快排），故时间复杂度为O(nlogn)，二分查找的时间复杂度为O(log2n)，最坏的情况是遍历了整个数组，即时间复杂度为O(n)，那么整体的时间复杂度为O(nlog2n)，效果上要优于冒泡排序的方式。

快排方式
```javascript
function getNum(arr, sum) {
    if (!Array.isArray(arr)) return null;

    arr.sort();

    for (var i = 0, j = arr.length - 1; i < j;) {
        if (arr[i] + arr[j] < sum) i++;

        else if (arr[i] + arr[j] > sum) j--;

        else return [arr[i], arr[j]];
    }

    return null;
}
```
43. 线程与进程，空间分配、资源分配等等
44. 三次握手、四次挥手及标志位、time-wait等等
45. H5的新特性，语义化
46. BOM与DOM，及BOM相关的一些属性
47. 写代码：双向绑定、防抖和节流
48. 设计模式：发布订阅、观察者
49. web worker，web storage，怎样验证本地数据的有效性
50. 缓存相关的http头部属性，强制缓存，协商缓存，优先级，以及meta标签
51. 怎样做的登录，接着就是session，cookie，token等等
52. input属性相关，以及怎样做的文件上传
53. transform transition与animation
54. 页面加载问题，JS的异步加载
55. 写代码：回文数，数组去重，自定义log，判断数据类型
56. 缓存命中率的问题，怎样确保缓存全部数据，缓存命中率不是100%应该怎么办
57. 说说性能优化的通用架构方案
58. 请求优化和渲染优化的方法
59. 编程，5个feach请求，请求完成后要求立即执行，但最终的输出顺序要按照要求输出ABCDE（思路是：将每个feach的回调通过a/a的方式输出，但最后没有run出来）
60. new一个对象过程发生了什么？
    1、创建一个新对象，如：var person = {};
    2、新对象的_proto_属性指向构造函数的原型对象。
    3、将构造函数的作用域赋值给新对象。（也所以this对象指向新对象）
    4、执行构造函数内部的代码，将属性添加给person中的this对象。
    5、返回新对象person。
61. css3特性中的transform：translateZ(0)有什么作用
GPU加速，优化前端性能
62. 列举三种禁止浏览器缓存的头字段，并写出响应的设置值
Expires：告诉浏览器把回送的资源缓存多长时间 -1或0则是不缓存
简要：添加Expires头能有效的利用浏览器的缓存能力来改善页面的性能，能在后续的页面中有效避免很多不必要的Http请求，WEB服务器使用Expires头来告诉Web客户端它可以使用一个组件的当前副本，直到指定的时间为止。
例如：Expires：Thu，15 Apr 2010 20：00：00 GMT; 他告诉浏览器缓存有效性持续到2010年4月15日为止，在这个时间之内相同的请求使用缓存，这个时间之外使用http请求。

Cache-Control：no-cache
Cathe-Control：max-age=315360000

Expires有一个非常大的缺陷，它使用一个固定的时间，要求服务器与客户端的时钟保持严格的同步，并且这一天到来后，服务器还得重新设定新的时间。
HTTP1.1引入了Cathe-Control，它使用max-age指定组件被缓存多久，从请求开始在max-age时间内浏览器使用缓存，之外的使用请求，这样就可以消除Expires的限制，
如果对浏览器兼容性要求很高的话，可以两个都使用。

Pragma：no-cache

63. 用js实现一个可以实现累加的函数add(1)(2)(3)
64. 说明在网页生命周期的所有阶段对性能优化的方案。
65. get和post的区别
66. 一亿条数据中如何快速的查找1000条最大的数据
65. 输入一个字符串，打印出字符串中首先出现的3个连续的数字

例如：

> N678cad89

> 678

```javascript
var readline = require('readline');
var readlineTest = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
readlineTest.on('line', function(line){
    let str = line;
    let reg = /\d+/g;
    console.log(str.match(reg));
    let arr0 = str.match(reg);
    let result = [];
    for(let i = 0; i < arr0.length; i++) {
        if (arr0[i].length >= 3) 
        {
            // console.log(arr0[i]);
            result.push(arr0[i]);
        }
    }
    if (result.length == 0) {
        console.log('false')
        return 'false';
    }
    if (result[0].length > 3) {
        console.log(result[0].slice(0, 3));
        return result[0].slice(0, 3);
    } else {
        console.log(result[0])
        return result[0];
    }
    readlineTest.close();
})
```

编程思路：先将字符串中的数字筛选出来，放入数组中，然后遍历数组，数组元素的长度是否超过2（大于等于3）, 若有，则输出第一个长度超过2的元素的前三位，否则输出无。

66. 实现两个大树相加的方法

例如：

> '1234567890123456789093232848777', '100000000'

> '1234567890123456789093332848777'


> 'null', '100000000'

> 'NaN'

```javascript
function add( a ,  b ) {
    // write code here
    // 定义a的长度
    let len1 = a.length;
    // 定义b的长度
    let len2 = b.length;
    // 若a的长度大于b，则扩充b的长度，在b的最高位之前补0，反之亦然。
    if (len1 > len2) {
        b = (Array(len1).join(0) + b).slice(-len1);
    } else {
        a = (Array(len2).join(0) + a).slice(-len2);
    }
    // 将a转为数组arr1
    let arr1 = a.split('');
    // arr1中的数字字符串格式化为数字，若出现非数字字符串，则转换为NaN
    arr1 = arr1.map(Number);
    // console.log(arr1);
    // 将b转为数组arr2
    let arr2 = b.split('');
    // arr2中的数字字符串格式化为数字，若出现非数字字符串，则转换为NaN
    arr2 = arr2.map(Number);
    // console.log(arr2);
    // 两数组内元素分别相加，并赋值为result
    let result = arr1.map((item, index) => {
        return item + arr2[index];
    })
    // 判断result中是否含有NaN，若有，则将NaN直接赋值为result
    for (let i = 0; i < result.length; i++) {
        if (isNaN(result[i])) {
            result = 'NaN'
            // console.log('NaN')
        }
    }
    // console.log(result)
    // 如果result的值为NaN，则输出result；否则，将result转为数字，并输出
    if (result == 'NaN') {
        console.log(result)
        return result;
    } else {
        result = result.join('');
        console.log(result);
        return result;
    }
}

// 测试例子
// "1234567890123456789093232848777","100000000"
var a = '1234567890123456789093232848777';
var b = '100000000';
var result = add(a, b);
console.log(result)
```

67. 找出字符串中最长的回文字串，并输出

例如：

> aabad

> aba


>cbbd

>bb

```javascript
function longestPalindrome( s ) {
    // write code here
    let deep = [];
    for(let i = 0; i < s.length; i++) {
        deep[i] = [];
    }
    let max = -1, str = '';
    for (let k = 0; k < s.length; k++) {
        for (let i = 0; i + k < s.length; i++) {
            let j = i + k;
            if (k == 0) {
                deep[i][j] = true;
            } else if (k <= 2) {
                if (s[i] == s[j]) {
                    deep[i][j] = true;
                } else {
                    deep[i][j] = false;
                }
            } else {
                if (deep[i + 1][j - 1] && (s[i] == s[j])) {
                    deep[i][j] = true;
                } else {
                    deep[i][j] = false;
                }
            }
            if (deep[i][j] && k > max) {
                max = k;
                str = s.substring(i, j + 1);
            }
        }

    }
    return str;
}

// let s = "aabad";
let s = "cbbd";
let result = longestPalindrome(s);
console.log(result);
```

编程题目持续更新......
