#预加载、预请求、预链接

## preload
- 高优先级加载资源
- 用于当前页面
- 
```
<link rel="preload" href="https://example.com/fonts/font.woff" as="font" crossorigin>
```
[doc](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preload)
[font special case](https://github.com/w3c/preload/issues/32)


## prefetch
- 低优先级域请求资源
- 用于下个页面
- 有三种不同的 prefetch 的类型，link，DNS 和 prerendering

```
<link rel="prefetch" href="/uploads/images/pic.png">
<link rel="dns-prefetch" href="//www.google-analytics.com"> 
<link rel="prerender" href="https://www.keycdn.com">
```

## preconnet
- 优先级未知
- 用于当前页下个页面
- 包括 DNS 解析，TLS 协商，TCP 握手

```
<link href="https://cdn.domain.com" rel="preconnect" crossorigin>
```

## 参考
[[译] 资源提示 —— 什么是 Preload，Prefetch 和 Preconnect？](https://juejin.cn/post/6844903646996480007)
