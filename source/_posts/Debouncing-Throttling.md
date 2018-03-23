---
title: 防抖动和节流阀
date: 2018-03-23 11:40:24
tags: 前端优化
---

------

看一个滚动的例子

<iframe height='500' scrolling='no' title='demo' src='//codepen.io/wangyuanlitin/embed/qojoGP/?height=300&theme-id=32936&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 60%;'></iframe>

在这个例子中，你会发现，当鼠标滚轮滚动的时，不管怎么控制，少则触发十几次，多则触发几十次，甚至几百次，
如果当前页面比较复杂，频繁的操作DOM会引起很大的性能问题

> 针对这种频繁触发（如scroll, resize, audio.ontimeupdate等）、短时间内多次调用，十分影响性能的操作，可以使用防止抖动和节流阀的处理方式


### 1. 防抖动
<!--more-->
原理：延迟处理，如果这中间有新的触发，则重新开始延时；最终将多次操作合并为一次，只处理最后一次触发。

使用场景： 窗口变化resize

<iframe height='500' scrolling='no' title='debounce' src='//codepen.io/wangyuanlitin/embed/YaQvvq/?height=300&theme-id=32936&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 60%;'></iframe>

> 1. 为scroll事件绑定处理函数
> 2. 每次事件触发前，都会清楚当前的timer，然后重新计算触发时间
> 3. 当scroll停止触发时，会在x毫秒后执行调用事件

underscore的实现：

```javascript
  /*
   * Underscore.js 1.8.3
   * @params func 执行方法
   * @params wait 延迟时间
   * @params immediate 是否是立即执行
   */
  _.debounce = function(func, wait, immediate) {
    var timeout, result;

    var later = function(context, args) {
      timeout = null;
      if (args) result = func.apply(context, args);
    };

    var debounced = restArgs(function(args) {
      // 如果当前有等待执行的事件，清除
      if (timeout) clearTimeout(timeout);
      // 设置新的timer时候，会判断immediate是不是立即执行
      if (immediate) {
        var callNow = !timeout;
        timeout = setTimeout(later, wait); // 这个没看懂没什么要在立即执行前要进行这个操作
        if (callNow) result = func.apply(this, args);

        // 等价于上面？？
        // if (callNow) {
        //   result = func.apply(this, args);
        // } else {
        //   timeout = setTimeout(later, wait);
        // }
      } else {
        // 设置新的timer
        timeout = _.delay(later, wait, this, args);
      }

      return result;
    });

    debounced.cancel = function() {
      clearTimeout(timeout);
      timeout = null;
    };

    return debounced;
  };
```

### 2. 节流阀

与防抖动最大的区别是，不管事件触发多频繁，都会在规定时间内执行一次事件处理函数

原理：1. 利用定时器，如果当前有待处理的函数，则不执行；如果没有则设置下一个定时器；保证在X毫秒内有一次触发

使用场景： 滚动加载

<iframe height='500' scrolling='no' title='EEXRJY' src='//codepen.io/wangyuanlitin/embed/EEXRJY/?height=300&theme-id=32936&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 60%;'></iframe>

> 1. 为scroll事件绑定处理函数
> 2. 每次事件触发前，会判断当前有没有正在等待的timer，如果有不设置，没有设置新的timer
> 3. 当事件执行后，可以设置新的timer

underscore的实现：

```JavaScript
  /*
   * Underscore.js 1.8.3
   * @params func 执行方法
   * @params wait 延迟时间
   * @params options 有两个属性 leading第一次触发 trailing最后一次触发
   */
  _.throttle = function(func, wait, options) {
    var timeout, context, args, result;
    var previous = 0;
    if (!options) options = {};

    var later = function() {
      previous = options.leading === false ? 0 : _.now();
      timeout = null;
      result = func.apply(context, args);
      if (!timeout) context = args = null;
    };

    var throttled = function() {
      var now = _.now();
      // 如果是第一次触发&&leading(第一次执行不是立即执行)为false，将当前时间赋值给previous
      if (!previous && options.leading === false) previous = now;
      var remaining = wait - (now - previous);
      context = this;
      args = arguments;
      // 如果是时间间隔到了，或者是时间间隔大于等待时间(可能是浏览器时间改了)
      if (remaining <= 0 || remaining > wait) {
        if (timeout) {
          clearTimeout(timeout);
          timeout = null;
        }
        previous = now;
        result = func.apply(context, args);
        if (!timeout) context = args = null;
        // 如果当前有等待处理的事件，并且最后一次需要触发
      } else if (!timeout && options.trailing !== false) {
        timeout = setTimeout(later, remaining);
      }
      return result;
    };

    throttled.cancel = function() {
      clearTimeout(timeout);
      previous = 0;
      timeout = context = args = null;
    };

    return throttled;
  };
```

### 3. 总结

debounce： 将事件合并成一次执行
throttle： X毫秒内执行操作