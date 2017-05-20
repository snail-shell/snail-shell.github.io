# Bootstrap之栅格化布局

标签（空格分隔）： Bootstrap使用笔记

---
### Bootstrap栅格化布局的含义
  先来写写bootstrap的栅格化布局,栅格化布局是bootstrap最基本的理念,也是bootstrap的一个创新.
  >Bootstrap 包含了一个响应式的、移动设备优先的、不固定的网格系统，可以随着设备或视口大小的增加而适当地扩展到 12 列。它包含了用于简单的布局选项的预定义类，也包含了用于生成更多语义布局的功能强大的混合类
 
### Bootstrap栅格化布局的使用

列标签要用在行标签里面,列标签里面使用`col-xs-*`,`col-sm-*`,`col-md-*`,`col-lg-*`(*代表的是数字).
使用时千万要注意列标签后的数字之和为12. 超过的内容会自动换行.影响排版

### Bootstrap栅格化布局的偏移列
>偏移是一个用于更专业的布局的有用功能。它们可用来给列腾出更多的空间。例如，`.col-xs-*` 类不支持偏移，但是它们可以简单地通过使用一个空的单元格来实现该效果。
为了在大屏幕显示器上使用偏移，请使用 `.col-md-offset-*` 类。这些类会把一个列的左外边距（margin）增加 * 列，其中 * 范围是从 1 到 11。

自己举个例子 看能不能听懂
某一行中只有一个列(`.col-md-4`),如果想让这个列居中显示,那么你需要设置偏移列`.col-md-offset-4`(设置原因:一行有12列,12减去你占用的4列还剩八列,在这八列中,你需要居中,你就必须要平分,这样得到四列)来进行居中

### Bootstrap栅格化布局的列嵌套
>为了在内容中嵌套默认的网格，请添加一个新的 `.row`，并在一个已有的 `.col-md-*` 列内添加一组 `.col-md-*` 列。被嵌套的行应包含一组列，这组列个数不能超过12（其实，没有要求你必须占满12列）。

    `<div class="col-md-9">
         <h4>第二列 - 分为四个盒子</h4>
         <div class="row">
            <div class="col-md-3">
               <p>Consectetur art party Tonx culpa semiotics. Pinterest </p>
            </div>
            <div class="col-md-9">
               <p> sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
            </div>
         </div>
         <div class="row">
            <div class="col-md-5">
               <p>quis nostrud exercitation ullamco laboris nisi ut </p>
            </div>   
            <div class="col-md-7">
               <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit</p>
            </div>
         </div>`
从上面的例子我们可以看到在`.col-md-9`中,它的区域中被嵌套两行,而这两行中的列数和刚好为12.这样显示起来就刚好占据`.col-md-9`的全部区域.不足12也行,但是没有占据.col-md-9的全部宽度,不太美观.

### Bootstrap栅格化布局的列排序
>Bootstrap 网格系统另一个完美的特性，就是您可以很容易地以一种顺序编写列，然后以另一种顺序显示列。
您可以很轻易地改变带有 .col-md-push-* 和 .col-md-pull-* 类的内置网格列的顺序，其中 * 范围是从 1 到 11。

详细解释下,真正在运用时`.col-md-push-*`和`.col-md-pull-*`后的数字一定是要交换之后的,不然情况特复杂. 先说第一种情况:
排序前和排序后基本一样,只是排序后的多了`.col-md-push-*`和`.col-md-pull-*` 示例就写排序后的代码.

    <div class="row">
          <p>排序后</p>
          <div class="col-md-5 col-md-push-7" 
             style="background-color: #dedef8;
             box-shadow: inset 1px -1px 1px #444, 
             inset -1px 1px 1px #444;">
             我在左边,可惜你也看不到我
          </div>
          <div class="col-md-7 col-md-pull-5" 
             style="background-color: #dedef8;
             box-shadow: inset 1px -1px 1px #444, 
             inset -1px 1px 1px #444;">
             我在右边
          </div>
       </div>

上面这个示例显示的是正常的互换.  如果改成`col-md-push-8`和`col-md-push-4`.这时列数之和是12.但是整体的这一行都往右侧偏移一列.
如果改成`col-md-push-7`和`col-md-push-4`.这时列数之和不是12,是11,(push是推的意思)那么在这一行十二列中,把`col-md-push-7`这一标签区域往后推一个列,在后面列不动的情况下,两者重叠一个列.
如果改成`col-md-push-6`和`col-md-push-3`.这种情况和上面一样,只不过推进去的列为3列.
如果改成`col-md-push-6`和`col-md-push-6`.这时列数之和是12.但是整体的这一行都往左侧偏移一列.
如果改成`col-md-push-5`和`col-md-push-7`.这时列数之和是12,但是这一行整体都往左侧推进两列.奇怪的是并没有重叠.
如果改成`col-md-push-5`和`col-md-push-5`.这时列数之和不为12,按照上面两列的习惯.这次应该是往左侧推,但这次`col-md-push-5`的标签区域没有变化,只不过是`col-md-pull-5`这一区域又减少两列的宽度(重叠).

这似乎是个有意思的现象.先下个结论试试,看能不能推翻.结论如下:
正常互换之后,
①当col-md-push-*这一数字增大时,col-md-pull-*不变的话,就会让两个标签块之间有间距( 此时的列数之和超过12).只有col-md-pull-*在减小,这一行就会往右侧偏移.(此时的列数之和小于等于12).
②当col-md-push-*这艺术字在减小时,col-md-pull-*不变的话,就会让这一行整体向左侧移动(此时的列数之和小于等于12).col-md-pull-*在增大时,两标签块之间就会有间距(此时的列数之和大于12).当c.col-md-pull减少的列数小于等于col-md-push减少的列数,那么col-md-push就回归到互换后的整成,而col-md-pull就会减少(重叠).col-md-pull减少的列数>col-md-push减少的列数.就像一个一个负数和一个整数相加,先化简,在求和.当然这里就是先重叠,再向左侧偏移.


  



