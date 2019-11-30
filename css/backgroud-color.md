# background-color的覆盖范围

>平时开发时很少有border-color为透明的情况，在遇到border-color为透明时发现background-color覆盖了border  

结论：background-color的范围是border-box。  

解决方法：使用背景裁剪  
`background-clip:padding-box;`