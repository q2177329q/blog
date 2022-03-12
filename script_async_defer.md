# script的async和defer属性
## 共同点
- 都是异步，不会阻塞dom 解析

## 不同点
- async先下载完成先执行；defer按照dom中顺序执行
- async执行顺序和DOM 解析完毕与否、DOMContentLoaded触发与否无关，defer会在DOM 解析完毕，DOMContentLoaded之前执行

## 动态插入脚本
- 默认行为如async
- async设置为false后和defer一样

## 写法示例
```
<script defer src="something.js"></script>
<script async src="something.js"></script>

<script>
  let script = document.createElement('script');
  script.src = "something.js";
  script.async=false
  document.body.append(script);
</script>
```

## 参考资料

- [脚本：async，defer](https://zh.javascript.info/script-async-defer)
- [图解 script 标签中的 async 和 defer 属性](https://juejin.cn/post/6894629999215640583)
