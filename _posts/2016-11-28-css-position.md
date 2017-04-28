---
layout: post
title: CSS position定位属性讲解
author: lijaha
category: blog
description: CSS系列，position定位标签
---

## CSS position定位属性讲解

### 0x1.position属性介绍

#### 1.浏览器支持

首先推荐个网站：[查询CSS浏览器兼容](https://www.quirksmode.org)

通过对position的查询我们可以知道：

![CSS](./images/CSS/css1.png)

也就是说IE8以上，及其他主流的浏览器都可以正常使用，WebKit中的minor bug请不要担心，因为该网站用的测试浏览器版本比较老。

#### 2.position定义

position中的定义，W3C中讲得蛮详细的，

![CSS](./images/CSS/css2.png)

上图中这两句话要特别注意：

 **1.任何元素都可以定位，不过绝对或者固定元素会生成一个块级框，而不论元素自身类型。**

 **2.相对定位元素会相对于它在正常流中的默认位置偏移。**

这第一句话的意思，不管元素原来是块级还是行内元素，只要使用了position中的绝对（absolute）和固定（fixed）属性值，都会变成块级元素，同样使用float属性也将会变成块级元素。

第二句话就是说使用position中的相对（relative）属性值是不会脱离正常的文档流，那么使用absolute和fixed就会脱离文档流。

#### 3.position的属性值：

**static：默认值，元素出现在正常的流中。**

**relative：生成相对定位的元素，相对于正常位置进行定位。**

**absolute：生成绝对定位元素，相对于static定位以外的第一个父元素进行定位。**

**fixed：生成绝对定位的元素，相对于浏览器窗口进行定位。**

**还有个inherit因为用得比较少，这里就不举例了。**

### 0x2.position属性值详解

#### 1.relative属性

没有使用position：

![CSS](./images/CSS/css3.png)

效果：

![CSS](./images/CSS/css4.png)

使用relative属性值：

![CSS](./images/CSS/css5.png)

从效果2的图片中我们可以清晰的看到，div3并没有因为div2的相对偏移而向上移动，也就是说div2原来所占据的位置有所保留，这也就解释了relative属性值不会脱离文档流而是在正常的流中偏移。

#### 2.sbsolute属性值：

absolute属性值在使用中**相对于static定位以外的第一个父元素进行定位。**

准备工作：

![CSS](./images/CSS/css6.png)

准备效果：

![CSS](./images/CSS/css7.png)

下面我们来设置div1的position为relative属性值，div2为static属性值，上文中说absolute是相对于static属性值以外的第一个( 设置position)父元素进行定位。那么我们设置的absolute属性值相对的位移应该就是div1。

![CSS](./images/CSS/css8.png)

absolute效果4：

![CSS](./images/CSS/css9.png)

从上图的效果我们可以看到红色框的absolute的位移是相对于绿色框的。同时对比效果3中的图，两个黑色的div框闭合到一起，即红色框的div不占有原来的位置，我们可以得出absolute属性值是脱离文档流的。

#### 3.fixed属性值：

![CSS](./images/CSS/css10.png)

fixed效果：

![CSS](./images/CSS/css11.png)

红色框的div的偏移是相对于浏览器的，同时两个黑色的div闭合到一起，也说明了fixed属性值是脱离文档流。
