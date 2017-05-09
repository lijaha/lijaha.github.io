---
layout: default
---

<body>
  <div class="index-wrapper">
    <div class="aside">
      <div class="info-card">
        <img class="logo" src="http://blogimage-1252049038.costj.myqcloud.com/logo.jpg" alt="logo" width="65px" height="65px"/>
        <h1>Lijaha</h1>
        <a href="http://www.jianshu.com/u/bb3bbe79b2a1" target="_blank"><img src="http://blogimage-1252049038.costj.myqcloud.com/jianshu.png" alt="jianshu" width="25"/></a>
        <a href="javascript:void(0)" onclick="show()"><img src="http://blogimage-1252049038.costj.myqcloud.com/wechat.png" alt="wechat" width="25" onclick="show()"/></a>
        <a href="https://github.com/lijaha" target="_blank"><img src="http://blogimage-1252049038.costj.myqcloud.com/github.png" alt="github.png" width="25"/></a>
        <div id="wechat">
          <img src="http://blogimage-1252049038.costj.myqcloud.com/lijahaTalk.jpg" width="120"/>
        </div>
      </div>
      <div id="particles-js"></div>
    </div>

    <div class="index-content">
      <ul class="artical-list">
        {% for post in site.categories.blog %}
        <li>
          <a href="{{ post.url }}" class="title">{{ post.title }}</a>
          <div class="title-desc">{{ post.description }}</div>
        </li>
        {% endfor %}
      </ul>
    </div>
  </div>
</body>
