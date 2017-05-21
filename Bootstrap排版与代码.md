# Bootstrap排版与代码

标签（空格分隔）： Bootstrap使用笔记

---
##前言
先说说Bootstrap默认使用的是什么字体,Helvetica Neue,Helvetica,Arial和sans-serif作为默认字体栈.
在这一个排版中,可以学到创建标题,段落,列表及其他内联元素.
###标题
> Bootstrap中定义了所有的HTML标题(h1-h6)的样式.

###内联子标题
> 如果需要向任何一个标题添加一个内联子标题,只需要简单地在元素两旁添加<small>,或者添加.small class,这样你就能得到一个字号更小的颜色更浅的文本.(不能继承前面的样式效果)<small>标签设置文本为父文本大小的85%.

示例:

    <h2>我是标题h2,<small>我是副标题</small></h2>
    <h2>我是标题h2,<span class="small">我是副标题</span></h2>
    
上面两个代码块的效果一样.

###引导主题副本
> 为了给段落添加强调文本,则可以添加class="lead",这将得到更大更粗,行高更高的文本. 
应用的话不可能整段整段的.应用的话可能会突出某一句话,所以给那一句话添加`<span class="lead"></span>`标签更好.

###缩写--------------(重要的技能)
>HTML元素提供用于缩写的标记,比如WWW或HTTP<abbr>元素的样式为显示文本底部的一条虚线边框,当鼠标悬停在上面时会显示完整的文本(只要你为<abbr>title属性添加了文本). 为了得到一个更小的字体,请添加一个.initialism到<abbr>.

示例

    <abbr title="World Wide Web">WWW</abbr>
    <br>
    <abbr title="Real Simple Syndication" class="initialign">RRS</abbr>
不能上图,好伤啊.
应用的话,需要去掉文本下侧中的虚线框.这样使用才会美观.(用border-bottom:0 none;设置一下,发现只能去掉一条虚线,也就是说还有一条虚线.刚才研究引用时.试了text-decoration:none;发现另外一条虚线也去掉喽.开心),也就是说这个标签可以用.  这里的设置可能会在后续有兼容问题!先放着.等有问题再回来一并处理.

###地址(Address)
> 使用`<address>`标签,您可以在网页上显示联系信息.由于`<address>`默认为`display:block;`您需要使用标签来为封闭的地址文本添加换行.   这里不明白,设置换行怎么就与`display:block`扯上关系?

留个备注.等以后能解决的时候再来.
使用这个标签可能是`<address>`标签中的段落间距比较合适.(暂且这样说,不然是在找不到合适的理由为什么要有`<address>`的存在)

###引用(Blockquote)
在任意的HTML文本旁使用默认的`<blockquote>`.其他选项包括,添加一个<small>标签来标示引用的来源,使用`class=pull-right`向右对齐引用.

示例

    <blockquote>
    <p>这是一个带有源标题的引用</p>
    <small>Someone famous in <cite title="Souce Title">Souce Title</cite></small>
    </blockquote>
    <blockquote class="pull-right">
    <p>这是一个带有源标题的引用</p>
    <small>Someone famous in <cite title="Souce Title">Souce Title</cite></small>
    </blockquote>

这上面的<p>标签是我添加上去的,它本来是没有的.没有标签也行么?搜索之后的结果:按照标准,最好放进入标签,当然如果你不放入标签,浏览器也能解析出来.作为文本节点.

---------------------------------------------

##小结 
目前引用和地址两个标签没有让我看到它们的应用场景,实在不知道怎么去介绍它们.唉,算喽,第一遍学就不要这么贪心.慢慢来吧.这些笔记我后面在再次读Bootstrap时再补充.

---------------------------------------------

###列表
> Bootstrap支持有序列表,无序列表和定义列表.
 有序列表:是指以数字或其他有序字符开头的列表
 无序列表:是指没有特定顺序的列表,是以传统风格的着重号开头的列表.如果你不想显示这些着重号,您可以使用`class=list-unstyled`来移除样式.您也可以通过使用`class=list-inline`把所有的列表项放在同一行中.
 定义列表:在这种类型的列表中,每个列表项可以包含<dt>和<dd>元素.<dt>代表定义术语,就像字典,这是被定义的属于(或短语).接着<dd>是<dt>的描述.您可以使用`class=dl-horizontal`把<dl>行中的属于与描述并排显示.
 
 示例

    <h4>定义列表</h4>
    <dl>
        <dt>Description 1</dt>
        <dd>Item 1</dd>
        <dt>Description 2</dt>
        <dd>Item 2</dd>
    </dl>  
    <h4>水平的定义列表</h4>
    <dl class=dl-horizontal>
        <dt>Description 1</dt>
        <dd>Item 1</dd>
        <dt>Description 2</dt>
        <dd>Item 2</dd>
    </dl>

定义列表中,什么都可以自己定义,这个很不错.配合上表单的一些属性.用去做表格就不错.

> 这里写一下其他排版的一些样式  
`class=text-justify`  设定文本对齐,段落中超出屏幕部分文字自动换行
`class=text-nowrap`   段落中超出屏幕部分不换行
`text-lowercase`      设定文本小写
`text-uppercase`      设定文本大写
`text-capitalize`     设定单词首字母大写
`pre-scrollable`      使`<pre>`元素可滚动scrollable

既然牵扯到`pre-scrollable`,那就说说代码在bootstrap中的显示.
> 第一种是<code>标签.如果你想要内联显示代码,那么您应该使用<code>标签.
  第二种是<pre>标签.如果代码需要被显示为一个独立的块元素或者代码有多行,那么您应该使用<pre>标签.
  请确保您在使用<pre>和<code>标签时,开始和结束使用了unicode变体:&lt;和&gt;.
  
最后一句意思是在`<code>`和`<pre>`标签中,你如果使用其他的标签,那么其他标签的<>要用&lt:和&gt;来代替.

示例

<p><code>&lt;header&gt;</code>作为内联元素被包围</p>
<p>如果需要把代码显示为一个独立的块元素,请使用&lt;pre&gt;标签:</p>

    <pre>
        &lt;article&gt;
        &lt;h1&gt;Article Heading;&lt;/h1&gt;
        &lt;article&gt;
    </pre>
    
    
    
不知道为什么<pre>内的内容效果在markdown中显示不出来.

