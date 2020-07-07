# OAuth 2.0的几种模式

OAuth的核心就是向第三方应用颁发令牌, 
第三方应用必须先在系统中申请client_id和client_secret.

四种模式:

- 授权码(authorization-code), response_type=code, grant_type=authorization_code, 
用户是在跳转到授权服务的页面时才输入账户信息进行登录, 登录成功后跳转回原应用, 安全性最高, 用于有后端服务的应用
- 隐藏式(implicit), response_type=token, 
用于没有后端的应用, 直接向前端颁发令牌, 令牌的位置是URL锚点(fragment, 以#表示), 而不是querystring. 
浏览器跳转时，锚点不会发到服务器，就减少了泄漏令牌的风险
- 密码式(password), grant_type=password, 
用户直接在应用中输入账户信息, 然后由应用发送到授权服务进行登录, 直接获取到token. 用于用户高度信任的应用.
- 客户端凭证(client credentials), grant_type=client_credentials, 用于没有前端的命令行应用, 直接获得该应用的token, 而非用户token.

## 参考

- [OAuth 2.0 的四种方式](https://www.ruanyifeng.com/blog/2019/04/oauth-grant-types.html)