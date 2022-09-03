首先，您需要透过 **/login API** 获得JWT token，然后每次客户端发送请求时，都需要在请求中携带该token。
如果token已过期，则可以透过 **/refreshToken** 以获取新的JWT token。需要通过您的后端服务进行询问/login和/refreshToken，不能直接从终端用户直接访问。

* 亦有提供匿名登入使用, 提供延迟盘口资讯, 详情请洽技术人员。

#### 如何使用JWT token
JWT token 必须包含在对API的每个请求的HTTP header中：

```
Authorization: Bearer JWT_Token
```

（将 "JWT_Token" 替换为您从[Login API](/j33app2/sports/wiki/Login-API)或 [RefreshToken API](/j33app2/sports/wiki/RefreshToken-API)收到的token。）
