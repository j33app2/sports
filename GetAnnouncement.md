用于透过指定时间区间获取区间内之平台公告。

## Request
```http request
GET
URI: /sports/{version}/GetAnnouncement?start=2021-02-01&end=2021-02-05&stickOption=0&language=en
Content-Type: application/json
Accept-Encoding: br, gzip, deflate
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```
| Parameter | Format | Mandatory | Description |
| ------ | ------ | ------ | ------ |
|start|Datetime|Yes|指定开始的日期时间 |
|end|Datetime|Yes|指定结束的日期时间<br>* 查询最长为七天|
|stickOption|int|--|查询一般公告或是特殊置顶公告 <br> 0 : 全部公告 (預設)<br>1 : 特殊置顶公告 <br>2 : 一般公告|
|language|string|--|指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table)<br>预设为英文 |

## Response
```
[
    {
        "messageId": int,
        "postTime": DateTime,
        "isSticky": bool,
        "message": string
    }
]
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
|messageId|int|公告讯息识别ID|
|postTime|DateTime|公告讯息张贴时间|
|isSticky|bool|是否为置顶公告|
|message|string|讯息公告内容|
