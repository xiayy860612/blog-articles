# 认证

当要访问一个系统之前, 必须先经过认证, 获取到系统中的用户后才能进行访问.
认证的目的是最终能够获取到在该系统中的用户的过程.

认证的核心元素:

- 凭证(credential/account)
- 会话(session/token)
- 用户(User)

## Credential/Account

凭证用于登录系统, 往往指某一类帐号, 例如

- 用户名|邮箱|手机号/密码
- 第三方帐号, 微信, github等

多个帐号可以对应到一个用户.

## Session/Token

会话的有效时间是用户在登录到系统后, 直到离开系统之前.
在有效时间里, 用户可以凭借会话去访问系统.

通过会话可以拿到用户信息.

会话的传递方式:

- Session in Cookie
- 透明Token in Header
  - Bearer Token
- 自包含Token in Header
  - JWT

### SSO(Single-Sign On)


## Context

- 请求上下文
- 会话上下文



## Reference

- [Authentication](https://en.wikipedia.org/wiki/Authentication)
- [OpenId Connect](https://openid.net/connect/)
- [SSO](https://en.wikipedia.org/wiki/Single_sign-on)
