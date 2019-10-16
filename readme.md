### 搭建javascrpt笔试/测试环境
有些前端笔试的编程中，编程语言是没有node.js，只有JavaScript，但是要求获取输入（多行或单行）并且要输出。但是本地vscode或html中没有相关环境可以测试代码/笔试。

如下图所示：
![截图](./static/cut1.png)

##### 下面的方法如何从0搭建一个可以测试JavaScript代码的环境：
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