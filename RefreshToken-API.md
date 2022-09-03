Token 有效時間為十分钟﻿, 十分钟内可重复使用

### Request
```http request
POST /refreshToken
Content-Type: application/json
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
```
#### **使用json方式将参数带入请求**

```json
{
    "vendor_id":"XXXXX",
    "vendor_member_id":"XXXXX"
}
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
| vendor_id | string | 厂商编号 |
| vendor_member_id | string | 会员编号 |

### Response
```json
{
    "access_token": "{JWT token}",
    "token_type": "Bearer"
}
```