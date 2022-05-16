# 跨域
## 同源策略
协议、域名、端口相同为同源

## 跨域
页面和请求接口不是同源的时候，为跨域请求。
跨域是浏览器安全策略，服务端无跨域一说。

## 解决跨域方法
* cors
* jsonp
### cors
[doc](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)

在请求跨域资源的时候，通过特定header的交互来确定是否被允许访问该资源。
* 如果请求是简单请求则直接发送真实请求，
* 如果请求不是简单请求，则会先发送预检请求（options），预检请求验证通过后发送真实请求

#### 请求头部
* Origin
* Access-Control-Request-Method
* Access-Control-Request-Headers： 真实请求要发送的header，逗号隔开

#### 响应头部
* Access-Control-Allow-Origin 和上面Origin对应。如果返回*，代表允许全部；返回具体域名时候，需要返回Vary: Origin
* Access-Control-Expose-Headers 如果js需要获取返回头中一些非基本头，需要在这里设置白名单列表，以逗号隔开
* Access-Control-Max-Age  预检请求多久有效，有效时间内，不重新发起预检请求。浏览器有默认有效时间，取返回值和浏览器值最小值
* Access-Control-Allow-Credentials  true代表可以带上cookie。和XMLHttpRequest.withCredentials = true对应
* Access-Control-Allow-Methods  允许的请求方法
* Access-Control-Allow-Headers  允许的头部

#### 简单请求
* get、post、head
* 请求头部只包含安全header，如：Accept、Accept-Language、Content-Language、Content-Type 
* Content-Type 的值仅限于下列三者之一：text/plain、multipart/form-data、application/x-www-form-urlencoded
* 请求中的任意 XMLHttpRequest 对象均没有注册任何事件监听器
* 请求中没有使用 ReadableStream 对象。
* 请求头部：origin，响应头部：Access-Control-Allow-Origin  协同完成跨域
* MLHttpRequest.withCredentials = true时候，如果Access-Control-Allow-Credentials不是true，请求被丢弃

#### 预检请求
|  请求头   | 响应头  |  描述  |
|  ----  | ----  | ---- |
| Origin  | Access-Control-Allow-Origin | 如果withCredentials=true,则不能返回*通配符      |
| Access-Control-Request-Method  | Access-Control-Allow-Methods | 如果withCredentials=true,则不能返回*通配符        |
| Access-Control-Request-Headers | Access-Control-Allow-Headers |    如果withCredentials=true,则不能返回*通配符     |
| 无  | Access-Control-Max-Age |        |
| 无，withCredentials=true  | Access-Control-Allow-Credentials |   如果简单请求，withCredentials=true但是没有返回true，返回被丢弃。如果预检请求没有返回true，失败     |
| 无  | Vary |  Access-Control-Allow-Origin不是*的时候需要返回Vary: Origin      |


#### 真实请求
|  请求头   | 响应头  |  描述  |
|  ----  | ----  | ---- |
| Origin  | Access-Control-Allow-Origin |       |
| 无  | Vary |        |

### jsonp
jsonp就是通过加载一个js，js内容是一个函数包含json内容。js加载完成后，调用这个函数获取数据。利用了js文件没有跨域限制的特性


