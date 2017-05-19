---
title: 每日算法之 － 冒泡排序
date: 2017-05-19 13:45:48
tags: [排序, 算法]
---


原理：比较相邻的两个元素，如果前一个比后一个大，则交换位置。

注意：是相邻，第二个和第三个比较，第三个和第四个比较

```javascript

function bubbleSort(array) {
  let length = array.length;
  for (var i = 0; i < length -1; i++) {
    for (var j = 0; j < length - 1-i; j++) {
      if (array[j] > array[j + 1]) {
        var temp = array[j];
        array[j] = array[j + 1];
        array[j+1] = temp;
      }
    }
    console.log(`第${i}轮排序: ${array}`);
  }
  return array;
}

let needSort = [5, 1, 2, 8, 5, 1, 9];
let res = bubbleSort(needSort);

```
<!--more-->
下面是犯错代码，现在好像也看不懂了

```javascript

function bubbleSort(array) {
  let length = array.length;
  for (var i = 0; i < length; i++) {
    for (var j = i; j < length; j++) {
      if (array[i] > array[j]) {
        var temp = array[i];
        array[i] = array[j];
        array[j] = temp;
      }
    }
    console.log(`第${i}轮排序: ${array}`);
  }
  return array;
}

let needSort = [5, 1, 2, 8, 5, 1, 9];
let res = bubbleSort(needSort);

```