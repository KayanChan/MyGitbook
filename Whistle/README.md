# Whistle的使用

@2019-05-16

@(Whistle教程)[web调试|代理|工具]



### 介绍

[官方文档传送门](http://wproxy.org/whistle/)

基于Node实现的跨平台web调试代理工具，主要用于查看、修改HTTP、HTTPS、Websocket的请求、响应，也可以作为HTTP代理服务器使用。

whistle采用的是类似配置系统hosts的方式，如`pattern opProtocol://opValue`

```bash
e.g.
www.example.com file:///User/test/dirOrFile
```

> pattern: 匹配请求url的表达式，可以为：域名，路径，正则及通配符等等多种匹配方式 ( www.example.com )
>
> opProtocol: 操作协议， 对应某类操作 ( file )
>
> opValue: 操作值， 对应具体操作的参数值 ( /User/test/dirOrFile )



### 安装启动

执行npm命令安装whistle `npm install -g whistle`

启动whistle `w2 start`

重启whsitle `w2 restart`

停止whistle `w2 stop`



### 配置代理

配置信息：

1. 代理服务器： `127.0.0.1`
2. 默认端口： `8899`

通过谷歌插件SwitchyOmega来配置代理，点击谷歌插件中的`选项`，`情景模式-proxy`设置代理服务器即可

```javascript
// 代理协议： HTTP
// 代理服务器： 127.0.0.1
// 代理端口： 8899
```



### 规则集合

打开[网址](http://127.0.0.1:8899/)，点击`create`就可以在规则集合里面书写规则了

##### 常用规则

```bash
#### 设置hosts
# https://www.baidu.com/ http://192.168.0.107/

#### 本地替换
# https://www.baidu.com/  D:\wamp\www\mb.html

#### 请求转发
# https://frontend.prod.dt-pf.com https://frontend.dev.dt-pf.com

#### 注入html、js、css(whistle会自动根据响应内容的类型，判断是否注入相应的文本及如何注入(是否要用标签包裹起来)。)
# http://192.168.0.107 html://D:\wamp\www\mb.html
# http://192.168.0.107 css://D:\wamp\www\libs\pure\0.6.2\pure-min.css
# http://192.168.0.107 js://D:\wamp\www\libs\digital_conversion\1.0.0\digital_conversion.js

#### 通过在pc上通过weinre修改网页的DOM结构及其样式,调试远程页面
# m.baidu.com weinre://test

#### 捕获日志
# m.baidu.com log://
```

> HTTPS、Websocket需要开启HTTPS拦截才可以正常抓包及使用所有匹配模式

