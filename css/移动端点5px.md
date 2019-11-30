# 移动端0.5px的问题
 
> 移动web设计中，在retina显示屏下网页会由1px会被渲染为2px(原理这里不详细解释，我们注重于解决方法)，即便都2018年了已经有不少的移动端支持0.5px但仍不能忽略兼容性，那么视觉稿中1px的线条还原成网页需要css定义为.5px  

解决方法：在dpr为2的前提下，使用transform缩放特性在伪元素中,现将width和height放大2倍，再缩小1/2。
 
``` scss
.box {
  position: relative;
  width: 0.84rem;
  line-height: 0.3rem;
  text-align: center;
  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 200%;
    height: 200%;
    border: 1px solid #CCCCCC;
    border-radius: 1rem;
    transform-origin: 0 0;
    transform: scale(0.5, 0.5);
    box-sizing: border-box;
    }
}    
```