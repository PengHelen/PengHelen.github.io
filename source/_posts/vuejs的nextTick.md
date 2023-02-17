---
title: vuejs的nextTick
date: 2023-02-08 10:38:46
tags: Vue
---

# 原因
Vue更新DOM是异步的

# 作用
回调被推迟到下一个DOM更新周期之后执行

# 语法
```
Vue.nextTick(function(){
  //...
})

mounted () {
  this.$nextTick(() => {
    /...
  });
  this.$nextTick().then(() => {
    /...
  });
}

async mounted () {
  await this.$nextTick(() => {
    //...
  });
}
```

# 使用场景
* `created`（dom还没渲染）中获取DOM的操作需要使用它
* 数据改变，改变DOM

# $nextTick VS setTimeout(fun,0)
`$nextTick` 在DOM更新后执行操作
`setTimeout(fun,0)` 回调在其他代码执行完之后（无论多长时间都等）立马执行

# 参考文献
[vue源码解读之vm.$nextTick](https://nlrx-wjc.github.io/Learn-Vue-Source-Code/instanceMethods/lifecycle.html#_3-vm-nexttick)

[$nextTick VS setTimeout](https://stackoverflow.com/questions/63669783/what-is-the-difference-between-using-vue-nexttick-vs-settimeout-0-in-vuejs)

[setTimeout(fn,0)](https://stackoverflow.com/questions/33955650/what-is-settimeout-doing-when-set-to-0-milliseconds/33963453#33963453)
