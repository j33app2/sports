此 API 用于获取指定时间区间内运动的赛果和优胜冠军赛果数量。
* 仅支持查询最近 12 天内的结果。

## Request
```http request
GET  /sports/{version}/GetSportResults?from=2022-01-01&until=2022-01-02&language=cs
Accept: application/json
Accept-Encoding: br, gzip, deflate
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```

| Parameter | Format | Mandatory | Description |
| ------ | ------ | ------ | ------ |
| from | DateTime | Yes |指定赛事开始日期(GMT+0)<br>日期字串格式應符合: "2021-01-01T00:00:00"(可 encode) |
| until | DateTime | Yes |指定赛事结束日期(GMT+0)<br>日期字串格式應符合: "2021-01-01T00:00:00"(可 encode) |
| language | string | |指定欲回应的数据语系，预设 "**en**".<br>请参阅 [Language Table](/j33app2/sports/wiki/Language-Table)|
## Response
```
{    
    "sportList": [
        {  
            "sportType": int,  
            "sportName": string, 
            "eventResults": int,
            "outrightResults": int
        }
    ]   
} 
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
| sportList | Array| 各体育赛果信息列表 |

| Parameter | Format | Description |
| ------ | ------ | ------ |
|sportType|int|体育项目ID|
|sportName|string|体育项目名称|
|eventResults|int|该体育项目的赛果数量|
|outrightResults|int|该体育项目的优胜冠军赛果数量|
