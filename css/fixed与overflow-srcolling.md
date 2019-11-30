# fixed与overflow-srcolling的冲突

> 当你给一个元素设置过position:fixed;后再增加-webkit-overflow-scrolling: touch;属性后，你会发现，滑动几次后可滚动区域会卡主，不能在滑动。
  

**解决方法**: 根据网上搜索出来的结果是若元素的position是absolute或relative,增加z-index的值，实测后无效，最后解决办法是将fixed移到父元素.