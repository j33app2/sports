此 API 用于获取指定时间区间内优胜冠军赛果信息。
* 仅支持查询最近 12 天内的结果。

## Request
```http request
GET  /sports/{version}/GetOutrightResults?from=2022-01-01&until=2022-01-02&language=cs
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
| query | string | |使用Odata指定特定格式的查询<br>预设查询**足球**| 

## Response
```
{    
    "result": [
        {
            "sportType": int, 
            "sportName": string,   
            "leagueId": int,  
            "leagueName": string, 
            "isTest": string,
            "outrights": [
                {
                   "eventTime": DateTime,
                   "teamId": int,
                   "teamName": string,
                   "status": string   
                }
            ]
        }
    ]   
} 
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
| result | Object Array| 优胜冠军信息列表 |

| Parameter | Format | Description | Queryable |  Query Example |
| ------ | ------ | ------ | ------ | ------ |
|sportType |int|体育项目ID|Yes|$filter=sporttype eq 1|
|sportName |string|体育项目名称|Yes|$filter=sportname eq 'Soccer' |
|leagueId |int|联赛ID|Yes|$filter=leagueid eq 56038 |
|leagueName |string|联赛名称|Yes|$filter=leaguename eq '*UEFA CHAMPIONS LEAGUE' or $filter=contains(leaguename,'NBA') |
|isTest |bool|是否为测试赛事|No| — |
|outrights |Object Array|优胜冠军详细信息|No| — |

| Parameter | Format | Description | Queryable |  Query Example |
| ------ | ------ | ------ | ------ | ------ |
|eventTime|DateTime|赛事时间 (时区GMT+0)|No| — |
|teamId|int|队伍ID|No| — |
|teamName|string|队伍名称|No| — |
|status|string|赛事状态<br>Won(赢), Lost(输), Refund(退款)|No| — |
