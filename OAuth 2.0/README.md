# OAuth2.0

@2019-05-27 10:01

@(知识点拓展类笔记)[OAuth2.0|授权|令牌]



### OAuth2.0是一种授权机制，用于颁发令牌

场景中的角色：客户端（第三方应用）、授权层（系统）、资源所有者（数据所有者）

数据所有者同意系统授权，**颁发一个短期且可复用的令牌（token）**，用来代替密码，供第三方应用使用，从而第三方应用可获取数据。

```flow
st=>start: 第三方应用想进入系统，获取数据，向系统申请授权

e1=>end: 第三方应用成功获得授权

e2=>end: 第三方应用获得授权失败

op1=>operation: 通过备案，数据所有者同意

op2=>operation: 系统产生令牌
(短期里可复用的供第三方使用token)

op3=>operation: 备案不通过，数据所有者拒绝

cond=>condition: 系统询问数据所有者，
根据客户端ID和密钥，
是否同意授权给第三方应用

input=>inputoutput: 第三方应用得到令牌

st->cond
cond(yes)->op1->op2->input->e1
cond(no,left)->op3->e2
```



### 令牌与密码（OAuth 2.0 的优点）

令牌既可以让第三方应用获得权限，同时又随时可控，不会危及系统安全。

1. 令牌是短期的，到期会自动失效，用户自己无法修改
2. 令牌可以被数据所有者撤销，会立即失效
3. 令牌有权限范围（对于网络服务来说，只读令牌就比读写令牌更安全）



### 四种授权方式

- 授权码（authorization-code）
- 隐藏式（implicit）
- 密码式（password）
- 客户端凭证（client credentials）



**授权码**为最常用的一种，安全性较高。使用场景：有后端的 Web 应用。

> 其他三种方式介绍前往：[资料](http://www.ruanyifeng.com/blog/2019/04/oauth-grant-types.html)

```flow
start=>start: 点击链接，从A网站跳到B网站

end=>end: A网站使用可以使用B网站授权的用户数据

sub1=>subroutine: 链接参数:返回的响应类型（授权码）、客户端ID、跳转地址、授权范围

op1=>operation: B网站要求用户登录,询问是否同意授权A网站

op2=>operation: 同意后，B网站跳转指定地址，把授权码传回

op3=>operation: A网站拿到授权码后，向B网站请求令牌

sub2=>subroutine: 链接参数: 客户端ID、客户端secret、授权方式、授权码、跳转地址

op4=>operation: B网站颁发令牌，返回一段JSON
(包含令牌： access_token和一些用户信息等)

start->sub1->op1->op2->op3->sub2->op4->end
```

