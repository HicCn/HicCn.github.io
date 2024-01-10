---
title: Hello World
tags : '测试'
categories : '其他'
data : 2022/11/3 16:35:24
aplayer : true
dplayer : true
---

### 这里是网站的开始，存根纪念。

Hello World
---
b站视频导入测试，并添加样式
<iframe  src="//player.bilibili.com/player.html?aid=53376920&bvid=BV174411L7ht&cid=93382155&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" style = "width: 100%;
    height: 30em;"> </iframe>

---

图片测试
{%  image
    url="/images/myBanner.jpg"
    title="带描述带图片"
%}

---

音频播放测试
{%  aplayer
    url="https://qiniu.sukoshi.xyz/public/music/鹿乃 - アイロニ.mp3"
    name="アイロニ"
    artist="鹿乃"
    cover="https://qiniu.sukoshi.xyz/public/music/鹿乃 - アイロニ.jpg"
    lrc="https://qiniu.sukoshi.xyz/public/music/鹿乃 - アイロニ.lrc"
    lrcType="3"
%}
---
视频测试
{%  dplayer
    url="https://qiniu.sukoshi.xyz/video/%E7%BE%8E.mp4"
    pic="https://qiniu.sukoshi.xyz/video/%E7%BE%8E.mp4?vframe/jpg/offset/10"
%}