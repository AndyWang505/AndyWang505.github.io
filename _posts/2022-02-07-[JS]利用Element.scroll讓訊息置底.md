---
layout: post
title:  "[JS] 利用Element.scroll讓訊息置底"
date:   2022-02-07 22:00:00 +0800
categories: JavaScript
tags: 實作 JavaScript
pin: false
---
一般在我們聊天的時候訊息的焦點都會自動固定在最下方追焦最新的訊息  

## 實作方法
### sample

![](https://i.imgur.com/23NCjo9.jpg)  

當我們送出訊息時，訊息的焦點應該要在底部，也是為方便使用者不用一直往下滾看最新訊息  

### Element.scrollHeight 

示意圖如下

![](https://i.imgur.com/SluCyyC.png)  

[圖片來源](https://developer.mozilla.org/zh-TW/docs/Web/API/Element/scrollHeight)

因為我們聊天室會使用overflow來隱藏超過聊天室高度的訊息並產生滾動條  

但如果要使焦點一直在底部，我們得知道超出外的內容有多少  

可以使用scrollHeight來得知超出捲軸的高度  

``` console.log(Element.scrollHeight); //Element是你想取得高度的元素```   

### Element.scrollTop

再來我們還要知道聊天室內容被捲動的距離，就是聊天室頂端及捲軸頂端之間的距離  

可以用scrollTop取得 

``` console.log(Element.scrollTop); //Element是你想取得距離的元素```  

### 自動置底完成

當我們知道scrollHeight及scrollTop時  

其實就可以把 "scrollHeight(超出的高)" 給 "scrollTop(內容頂端及捲軸頂端之間的距離)"  

```javascript
Element.scrollTop = Element.scrollHeight;
```  

這樣一來當我們新增一筆訊息scrollTop就會一直取得scrollHeight更新距離  

讓訊息焦點保持在底部！  

![](https://i.imgur.com/LdY1BSt.png)  
  
### #補充

關於scroll語法其他還有  

寬高
* scrollWidth / scrollHeight
* clientWidth / clientHeight
* offsetWidth / offsetHeight  

相對位置
* scrollLeft / scrollTop
* clientLeft / clientTop
* offsetLeft / offsetTop

##### 以上皆為記錄自己實作歷程，僅供參考與複習使用。