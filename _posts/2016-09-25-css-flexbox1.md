---
layout: post
title: Flex布局实例1：典型三栏布局
author: lijaha
category: blog
description: Flex布局实例1：典型三栏布局
---

    <!DOCTYPE html>
      <html>
        <head>
          <style type="text/css">  
            .container {  
              display: flex;  
              flex-flow: row wrap;  
              font-weight: bold;  
              text-align: center;  
            }
            .container >*{
              padding:10px;
              flex:1 100%;
            }
            .header{
              background-color:tomato;
            }
            .footer{
              background-color:lightgreen;
            }
            .main{
              text-align:left;
              background-color:deepskyblue;
            }
            .aside-1{
              background-color:gold;
            }
            .aside-2{
              background-color:hotpink;
            }
            @media all and(min-width:600px){
              .aside{
                flex:1 auto;
              }
            }
            @media all and(min-width:800px){
              .main{
                flex:2 0px;
              }
              .main{
                order:2;
              }
              .aside-1{
                order:1;
              }
              .aside-2{
                order:3;
              }
              .footer{
                order:4;
              }
            }
              </style>
            </head>
            <body>
              <div class="container">
                <header class="header">Header</header>
                <article class="main">
                  <p>
                    Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo.
                  </p>
                </article>
                <aside class="aside aside-1">Aside-1</aside>
                <aside class="aside aside-2">Aside-2</aside>
                <footer class="footer">Footer<footer>
              </div>
            </body>
          </html>

![](http://upload-images.jianshu.io/upload_images/3282997-a65c332027276a4c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3282997-2686ce8c6581d242.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
