# node.js之异步式I/O

标签（空格分隔）： node.js使用笔记

---

> node.js最大的特点就是异步式I/O(或者非阻塞I/O)与时间紧密紧密结合的编程模式.这种模式与传统的同步式I/O线性的编程思路有很大的不同,因为控制流在很大程度上要靠事件和回调函数来组织,一个逻辑要拆分若干个单元

### 阻塞与线程
> 什么是阻塞(block)呢?线程在执行中如果遇到磁盘读写或网络通信(统称为I/O操作),通常要耗费较长的时间,这时操作系统会剥夺这个线程的CPU控制权,使其暂停执行,同时将资源让给其他的工作线程,这种线程调度方式成为 <span class='lead'>阻塞</span>.
当I/O操作完毕时,操作系统将这个线程的阻塞状态解除,回复其对CPU的控制权,令其继续执行.这种I/O模式就是通常的同步式I/O(Synchronous I/O)或阻塞式I/O(Blocking I/O).
异步式I/O(Asynchronous I/O)或非阻塞式I/O(Non-blocking I/O)则针对所有I/O操作不采用阻塞的策略.当线程遇到I/O操作时,不会以阻塞的方式等待I/O操作的完成或者数据的返回,以事件的形式通知执行I/O操作的线程,线程会在特定时候处理这个事件.为了处理异步I/O,线程必须有时间循环,不断地检查有没有未处理的事件,依次予以处理.

稍微整理下,这样比较方便看懂.
>阻塞模式下,一个线程只能处理一项任务,要想提高吞吐量必须通过多线程,因为一个线程阻塞时还有其他线程在工作,多线程可以让CPU资源不被阻塞中的线程浪费.
而非阻塞模式下,一个线程永远在执行计算操作,这个线程所使用的CPU核心利用率永远是100%,I/O以事件的方式通知.线程不会被I/O阻塞,永远在利用CPU.
多线程带来的好处仅仅是在多核CPU的情况下利用更多的核,而Node.js的单线程也能带来同样的好处.(好处就是提高吞吐量)

上面一段话给我几个问题,什么叫做CPU核心利用率,CPU资源,吞吐量?
自己理解:CPU内部有多个核,一般而言的CPU利用率是指多个核结合一起的CPU(完整)的利用率,而CPU核心使用率默认是指单核.
CPU资源其实就是运行程序占用CPU使用率.
吞吐量是指系统在单位时间内处理请求的数量.


## 回调函数
Node.js异步读取一个文件
示例

    //readfile.js
    //异步的方式读取一个文件
    var fs=require('fs');
    fs.readFile('file.txt','utf-8',function(err,data){
    	if(err){
    		console.error(err);
    	}else{
    		console.log(data);
    	}
    })
    console.log('end.')
    
    运行的结果是
    end.
    this is file.txt(file.txt文件内容)
### 导读
异步式读取文件稍微有些违反直觉,`.end`先被输出. 
在Node.js ,异步式I/O是通过回调函数实现的.fs.readFile接收了三个参数,第一个是文件名,第二个是编码方式,第三个是一个函数,我们趁这个函数为回调函数.
javascript支持匿名的函数定义方式,譬如我们例子中回调函数的定义就是嵌套在fs.readFile的参数表中的.

    //readfilecallback.js
    function readFileCallBack(err,data){
        if(err){
            console.error(err);
            }else{
            console.log(data);
            }
    }
        var fs=require('fs');
        fs.readFile('file.txt','utf-8',readFileCallBack);
        console.log(end.);

Node.js同步读取一个文件

    // readfilesync
    // 同步读取文件
    var fs=require('fs');
    var data=fs.readFileSync('file.txt','utf-8');
    console.log(data);
    console.log('end.')
    
    运行的结果是
    this is file.txt
    end.
Node.js不鼓励使用同步I/O.
### 同步式与异步式小结
同步式读取文件的方式将文件名作为参数传入fs.readFileSync 函数,阻塞等待读取完成后,将文件的内容作为函数的返回值赋给data变量.接下来控制台输出data的值,最后输出`end.`
fs.readFile调用时所做的工作只是将异步式I/O请求发送给操作系统,然后立即返回并执行后面的语句,执行完以后进入时间循环监听事件.当fs接收到I/O请求完成的事件时,事件循环会主动调用回调函数已完成后续工作.因此我们会先看到`end.`,再看到file.txt文件的内容








