此API用于获取每个联赛中的赛事数量

## Request
```http request
GET  /sports/{version}/GetLeagues?from=2021-02-28&language=cs
Accept: application/json
Accept-Encoding: br, gzip, deflate
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```

| Parameter | Description |
| ------ | ------ |
| query | 使用Odata指定特定格式的查询 |
| from | 指定赛事开始日期，可以单独输入<br>日期字串格式應符合: "2021-01-01T00:00:00"(可 encode) |
| until | 指定赛事结束日期，可以单独输入<br>日期字串格式應符合: "2021-01-01T00:00:00"(可 encode) |
| language | 指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |

## Response
```
{    
    "leagues": League[]   
} 
```
| Name| Format | Description |
| ------ | ------ | ------ |
| leagues | array| 联赛讯息列表 |

### **League**
```
{
    "leagueId": int,
    "leagueName": string,
    "sportType": int,
    "sportName": string,
    "liveGameCount": int,
    "gameCount": int,
    "isParlay": bool
} 
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
| leagueId | int | 联赛ID | Yes | $filter=leagueid eq 56038|
| leagueName | string | 联赛名称 | Yes | $filter=leaguename eq '*UEFA CHAMPIONS LEAGUE'  or $filter=contains(leaguename,'NBA')|
| sportType | int | 体育项目ID | Yes | $filter=sporttype eq 1|
| sportName | string | 体育项目名称 | Yes | $filter=sportname eq 'Basketball'|
| liveGameCount|int|该联赛的滚球赛事数量|No|—|
| gameCount | int | 该联赛的非滚球赛事数量 | No | —|
| isParlay | bool | 是否为串关赛事 | Yes | $filter=isparlay eq true|
