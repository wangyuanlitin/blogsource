---
title: 折半查找
date: 2018-06-27 15:25:06
tags: [算法, 查找]
---

------

前提:　数据必须是已排序的
基本思想：取中间的值，与要查找的值进行对比
　　　　　如果中间值等于要查找的值，则中断查找
　　　　　如果大于要查找的值，则在左侧继续查找，
　　　　　如果小于要查找的值，则在右边继续查找
　　　　　循环执行上述操作，直到找到目标值为止

```javascript
function find(data, value) {
  if (!Array.isArray(data)) { return '序列不是数组' }

  let left = 0 // 开始下标
  let right = data.length - 1 // 结束下标
  
  let pos

  while (left <= right) {
    let mid = parseInt((left + right)/2)
    let data_mid = data[mid]
    if (data_mid === value) {
      pos = mid
      break
    } else if (data_mid > value) {
      right = mid - 1
    } else {
      left = mid + 1
    }
  }
  return pos
}

var data = [1, 2, 3, 5, 7, 11, 23, 12313]
var pos = find(data, 232)
console.log(pos)
pos = find(data, 1)
console.log(pos)
pos = find(data, 12313)
console.log(pos)
```