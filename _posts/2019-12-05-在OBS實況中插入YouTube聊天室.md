---
title: "在OBS實況中插入YouTube聊天室"
date: 2019-12-05
last_modified_at: 2019-12-05
categories:
  - blog
tags:
  - 實況
  - OBS
  - YouTube
permalink: /blog/2019_12_05_01
---
### 1. 獲得直播的URL

在直播信息左下角分享中可以找到直播的URL例如
```
https://www.youtube.com/channel/UC_NpCQY-99aJGsRt99tcVsw/live
```
如果有自定義網址格式會是這樣
```
https://www.youtube.com/c/Channel/live
```
### 2. 獲得聊天室的URL

因爲每次YouTube直播聊天室URL都會變動,所以我們需要其他網站幫我們自動獲得聊天室URL,比如下面這個:
```
http://bigmond.co.uk/p/youtube_chat.php?channel=https://www.youtube.com/channel/UC_NpCQY-99aJGsRt99tcVsw/live
```
?channel=之後為第一步獲得的直播URL
### 3. 將聊天室URL添加到OBS
- 打開OBS,添加瀏覽器源
![](/assets/images/2019_12_05_01/2019_12_06_001849.jpg)
- 在URL中輸入第二步中的URL
![](/assets/images/2019_12_05_01/2019_12_06_001544.jpg)
- 點擊確定,確認能在畫面中顯示自己的聊天室.
![](/assets/images/2019_12_05_01/2019_12_06_003559.jpg)
### 4. 設置聊天室樣式

在網站https://chatv2.septapus.com/中可以設置聊天室樣式,并在最下面的css框中複製生成出的代碼,將複製出來的代碼粘貼到第三步添加的聊天室輸入源中的自定義CSS中<br>
![](/assets/images/2019_12_05_01/2019_12_06_003748.jpg)
點擊確定即可看到最終效果
![](/assets/images/2019_12_05_01/2019_12_06_003846.jpg)