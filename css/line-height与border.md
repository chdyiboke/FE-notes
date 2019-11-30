# line-height 与 border

> 如果为一个div设置border，同时又试图使用line-height让元素内的字体居中，会如下图所示，字体会稍稍偏下。
  
<div >
  <div style="border:5px solid #000; line-height:40px;height:40px;width:80px;text-align:center; margin:0 auto;">文字</div>
</div>  
  
    

**解决方法**：类似border `0.5px`的解决方案，使用`::after`的方式重新画一个出来。

**原理**：line-height用来定义 __行高__ ，而使用将line-height的属性赋值与height相同的值，本质上是使文本组成的行框的行高等于容器的高度，文本在选框中居中。若设置border并且是`box-sizing:border-box;`的状态,则line-height是不等于height的，所以文本稍稍偏下。  
由此得到另一种解决方案 **box-sizing:content-box;**

---
__另外__：对于line-height有一个经典问题：1.5与150%的区别？  
`ling-height:1.5`是根据子元素的`font-size`来计算并设置子元素的line-height  
`ling-height:150%`是根据父元素的`font-size`来计算并设置子元素的line-height