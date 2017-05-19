---
title: 计算字符串中每个字母出现的次数
date: 2015-05-19 09:53:12
tags: 代码片段
---


```javascript

function calculateLetterTimes(e_string) {
  let charObject = {};

  // 循环拿到每个单词出现的次数
  for (let i = 0; i < e_string.length; i++) {
    charObject[e_string[i]] = charObject[e_string[i]] || 0;
    charObject[e_string[i]] += 1;
  }

  let max_count = 0;
  let res = {};

  // 拿到出现频率最大的单词
  for (var key in charObject) {
    let char_count = charObject[key];
    if (char_count > max_count) {
      max_count = char_count;
      res = {};
      res[key] = char_count;
    }
  }

  // {"a": 12} 返回结果，a出现12次
  return res;
}


```