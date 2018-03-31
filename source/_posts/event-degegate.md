---
title: 事件－内存与性能
date: 2018-03-30 14:06:26
tags: JavaScript
---

------

在JavaScript中，添加到頁面上的事件處理程序數量直接關系到頁面的整體運行性能
主要原因:
1. JavaScript中，每個函數都是對象，都会占用内存；內存中的创建的對象越多，性能就越差
2. 過多的DOM操作，會延遲整個頁面的交互時間

如何利用好事件處理程序，也会有效提高性能问题

### 1. 事件委托

對"事件處理程序過多"問題的解決方案就是市建委託,事件委託利用了事件冒泡,只指定一個事件處理程序,就可以管理同一類型的所有事件

```javascript
// 例1
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ul>
```
<!--more-->

例1中，包含三個點擊後執行操作的列表，需要在點擊以後突出显示當前的li
如果按照最原始的做法，就是給每一個li都綁定一個click事件，當li触发了click事件，高亮當前行，其他行置灰

這只是一個簡單的列表，但是如果li有很多呢？如果還用這種方式，一來會導致代碼兩加大，二來難以維護, 最主要的問題就是創建了很多對象，佔用內存

更进一步，再優化一下，就是用事件委託，將click事件绑定在更高一級上，比如在这个例子中，可以將事件委託給父級ul處理，由於所有的li元素都是ul的子元素，在事件冒泡階段，click事件之後會被ul上的事件處理

與未使用事件委託相比，這種方式只取了一個DOM元素，只添加了一個事件，對用戶來說，效果沒有差別, 但是与技术来说內存佔用更少

### 2. 移除事件处理程序

每當將事件處理程序指定給元素時，運行中的瀏覽器代碼與JavaScript之間就會建立一個连接，连接越多，頁面執行就越慢，所以就需要在不使用的時候，及時處理這些"空事件處理程序"

```JavaScript
// 例2
<div id='div'>
  <input type='button' value='Click' id='btn'>
</div>
<script type='text/javascript'>
  var btn = document.getElementById('btn')
  btn.onclick = function () {
      document.getElementById('div').innerHTML = 'loading ......'
  }
<script>
```

例2中，btn被點擊後，会将div替換成一段文字，替换后，事件處理程序依然與按鈕保持這引用關系，但是在一些瀏覽器中，很有可能元素和事件應用還在內存中(沒有去驗證現代瀏覽器中是不是還有這種問題)，這種情況下最好的辦法就是手動刪除了

```JavaScript
<div id='div'>
  <input type='button' value='Click' id='btn'>
</div>
<script type='text/javascript'>
  var btn = document.getElementById('btn')
  btn.onclick = function () {
      btn.onclick = null // 移除事件處理程序
      document.getElementById('div').innerHTML = 'loading ......'
  }
<script>
```

移除事件處理程序，這樣就確保了內存可以被再次利用

### 3. 總結 

在使用事件时候要考虑以下内存与性能问题
1. 需要限制一个页面中事件处理程序的数量，数量太多会导致占用大量内存，而且也会让用户觉得页面反映不流畅
2. 事件委托，可以有效地减少事件处理程序的数量
3. 建议在浏览器卸载页面之前移除页面中所有的事件处理程序