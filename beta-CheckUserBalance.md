此API用于获取会员余额信息

## **Request**
```http request
GET /betting/{version}/CheckUserBalance
Content-Type: application/json
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```

## **Response**
```
{
    "currency": int,
    "balance": decimal,
    "outstanding": decimal
}
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
|currency|int|币别ID，请参阅 **[Currency Table](/nextfortune-evo/SportsbookClientAPI_CN/wiki/Currency_Table)**.|
|balance|decimal|用户余额|
|outstanding|decimal|用户预扣金额|