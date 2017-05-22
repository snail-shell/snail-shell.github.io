# node.js之上手笔记

标签（空格分隔）： node.js使用笔记

---

##运行node.js
 在运行之前,你需要安装node.js安装包,新手千万别作死去编译.然后下载一个python软件.(版本号大于2.5,但要小于3.0)安装python时,一定把环境变量功能添加进去,不然呢等下还要手动添加.对于书中提到的Visual stdio 之类的我没有安装,上学期学习的时候,安装了一个,不知道卸没卸载完全.头大!
 接下来开始写吧,打开编辑器软件,新建一个文件名为Hello.js(记住这个文件所在的目录),在其中编写`console.log('Hello World');`.进入doc界面(windows的).cd xxx(xxx 是Hello.js的目录路径).接下来运行`node Hello.js`.这时你会见到Hello.js中的Hello World.

node --help功能很好,可以花时间多看看.
node-e"console.log('Hello world');"这也是一条执行语句,把要执行的语句作为node-e的参数直接执行.
这里面还要注意一个小问题,在输入时,不要只输入单标点,还要注意使用双标点.

运行node.js程序的基本方法就是执行node script.js,其中script.js是脚本的文件名.(事实上,脚本文件的扩展名不一定是.js,例如我们将脚本保存为script.txt,使用node script.txt命令同样可以运行.扩展名使用.js只是一个约定而已,遵循了javascript脚本一贯的命名习惯.)

### node的REPL模式
> REHL(Read-eval-print loop),即输入-求值-输出循环,就会知道在终端下运行无参数的python命令或者使用Python IDLE打开的shell,可以进入一个即时求值的运行环境.Node.js也有这样的功能.运行无参数的node将会启动一个javascript的交互式shell:(这些具体点可以在网上找到,我觉得我暂时还不需要掌握这么多.没时间啊)

## 建立HTTP服务器
> 建立一个app.js文件,内容为:

    var http=require('http');
    http.createServer(function(req,res){
    	res.writeHead(200,{'content-type':'text/html'});
    	res.write('<h1>Node.js</h1>');
    	res.end('<p>Hello World</p>');
    }).listen(3000);
    console.log("HTTP server is listening at port 3000.");

然后执行node app.js命令,会输出`HTTP server is listening at port 3000.`.然后浏览器打开`http://127.0.0.1:3000`,就会看到<h1>Node.js</h1> <p>Hello World</p> 这两个文本

> 原因:如上所述,用node.js实现最简单的HTTP服务器.这个程序调用Node.js提供的http模块,对所有的HTTP请求答复同样的内容并监听3000端口.并且在doc界面中,并没有退出.而是一直等待,直到按下Ctrl+C才会结束.因为listen函数创建了事件监听器,使得Node.js进程不会退出事件循环.






