---

layout: post
title: 《高性能响应式Web开发》笔记
category: blog
author: lijaha
description: 《高性能响应式Web开发》笔记

---

1.设计人员希望以页面的宽度来渲染页面，并能自然自适应到系统宽度，于是手机厂商提供了一个名为viewport的<meta>标签设置视口大小，
><meta name=“viewport” content=“width=XXX”>
>通过content属性中设置width参数，也可以添加initial-scale参数来控制渲染时缩放视口的比例>如果未设置该参数，浏览器会自动将页面缩放至与浏览器宽度一致，通常设置为initial-scale=1.0;
><meta name=“viewport” content=“width=XXX,initial-scale=1.0”>
>因不同的设备的系统分辨率不一样，即时在同一种设备上，横竖两种握持方式也会让渲染方式不同
><meta name=“viewport” content=“width=device-width, initial-scale=1.0”>

2.查询HTML5在不同浏览器中的支持情况：[caniuse](http://www.caniuse.com)
   查询其他非HTML5标准样式和脚本特性在不同浏览器的兼容情况：[quirksmode](http://www.quirksmode.org/compatibility.html)

3.媒体查询匹配顺序，由后向前匹配，匹配成功立即终止。

4.媒体查询移动优先，即希望页面优先采用移动样式，它的特征是使用min-width匹配页面宽度，默认是最窄的情况，再依次考虑设备屏幕逐渐变宽。
> (宽度为320px以下)
html{
}
(宽度为320px-1024px)
@media(min-width:320px;){
}
(宽度为1024px以上)
@media(min-width:1024px;){
}

5.媒体查询桌面优先，采用max-width判断页面宽度匹配的情况，首先考虑的是在一般桌面上的效果，再依次递减宽度，考虑更窄的设备上的场景。
(设备屏幕宽度大于1024px)
> html{
}
(设备屏幕宽度在320-1024px)
@media(max-width:1024px;){
}
(设备屏幕宽度在320px以下)
@media(max-width:320px;){
}

6.CSS3新单位vh和vw，vh全称为视口高度，，1vh等于1%的当前浏览器视口高度，1vw相当于1%的当前浏览器视口宽度，而vmax和vmin分别表示指在视口高度和宽度中的最大和最小值。

7.background-size属性为cover，意为保持在图片长宽比的基础上缩放背景图像，使其尽可能完整地覆盖背景。

8.sizes和srcset属性结合使用:
> sizes=“(max-width:640px) 100vw,(max-width:960px) 50vw,calc(100vw/3)”  srcset=“large.jpg 1024w, meidum,jpg 640w, small.jpg 320px”  
sizes语法：
sizes=“[media query] [length],[media query] [length]…[length] etc"

SIZES属性值是由一系列由逗号隔开的描述图片宽度的表达式组成，每一组包含两部分：[media query]代表匹配的查询条件，[length]代表该查询条件下图片所占用的宽度。最后一个表达式可以只描述图片大小，表示在默认查询条件下的图片占用宽度。

9.image-set属性主要用于为容器背景图片提供高清图片支持，语法与媒体查询类似，不过图片地址后面只能跟随设备的像素比条件，而且在使用image-set最好加上浏览器厂商的前缀:
> background-image:-webkit-image-set(url(XXX.PNG)) 2x

如在网络环境较差的情况下，高清设备可能会选择加载低清图片。

10.渐进式图片，浏览器接收到图片后都是将图片从上至下渲染，而渐进式渲染是浏览器利用已有、接收到的数据首先渲染出一个分辨率较低或者比较模糊的图片版本，再根据接收到的图片数据补充完善使图片更加清晰。

11.回流：当页面上的某个元素的大小或者位置发生更改时，都会影响到与它相邻元素状况，甚至整个页面的元素状态(位置、元素大小)都需要重新计算和更新。一个页面至少会有一次回流，就是在页面初始化时。

12.重绘：当某个元素颜色样式发生更改时(如背景颜色、文字颜色)，页面也需要更新，浏览器需要重新绘制元素。

13.重排：页面的布局发生变化需要重新生成布局，重绘不一定会重排，重排一定会重绘。
