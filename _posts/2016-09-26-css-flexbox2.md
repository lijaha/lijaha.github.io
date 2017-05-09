---
layout: post
title: Flex布局实例2：自适应导航栏
author: lijaha
category: blog
description: Flex布局实例2：自适应导航栏
---

      <!DOCTYPE html>
        <html>
          <head>
            <style type="text/css">
              .box{
                margin:0px;
                background-color:deepskyblue;
                display:flex;
                flex-flow:row wrap;
                justify-content:flex-end;
                list-style:none;
              }
              .box a{
                text-decoration:none;
                display:block;
                color:white;
                padding:1em;
              }
              .box a:hover{
                background-color:#00AEE8;
              }
              @media all and(max-width:800px){
                .box{
                  justify-content:space-around;
                }
              }
              @media all and(max-width:600px){
                .box{
                  flex-flow:column nowrap;
                  padding:0;
                }
                .box a{
                  text-align:center;
                  padding:10px;
                  border-bottom:1px solid rgba(0,0,0,0.1);
                }
                .box li:last-of-type a{
                  border-bottom:0px;
                }
              }
              </style>
            </head>
            <body>
              <ul class="box">
                <li><a href="#">Home</a></li>
                <li><a href="#">Product</a></li>
                <li><a href="#">Connect</a></li>
                <li><a href="#">About</a></li>
              <ul>
            </body>
          </html>

大屏：
![](http://upload-images.jianshu.io/upload_images/3282997-1854d6aa8d261792.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

800中屏：
![](http://upload-images.jianshu.io/upload_images/3282997-a19ca8479c57a407.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
600小屏：
![](http://upload-images.jianshu.io/upload_images/3282997-6231b2955e78aab3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
