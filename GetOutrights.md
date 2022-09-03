此API用于获取优胜冠军赛事信息。

## Request
```http request
GET  /sports/{version}/GetOutrights?language=cs
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
    "outrights": Outright[]   
} 
```
| Name| Format | Description |
| ------ | ------ | ------ |
| outrights | array| 优胜冠军信息列表|

### **Outright**
```
{
	"sportType": int,
	"sportName": string,
	"leagueId": int,
	"leagueName": string,
	"eventCode": string,
	"lDisplayMode": int,
	"eventDate": DateTime,
	"outrightStatus": string,
	"isTest": bool,
	"leagueGroup": string,
	"teams": Team[]
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|sportType|int|体育项目ID|Yes|$filter=sporttype eq 1|
|sportName|string|体育项目名称|Yes|$filter=sportname eq 'Soccer'|
|leagueId|int|联赛ID|Yes|$filter=leagueid eq 93816|
|leagueName|string|联赛名称|Yes|$filter=leaguename eq '*UEFA EURO 2020 - WINNER'  or $filter=contains(leaguename,'UEFA')|
|eventCode|string|赛事标识符|No|—|
|lDisplayMode|int|指定联赛的显示模式。<br>0：All<br> 1：Olympic<br> 2：World Cup<br> 3：Euro<br> 4：Winter Olympic<br> 5：COPA America|No|—|
|eventDate|DateTime|赛事日期|No|—|
|outrightStatus|string|优胜冠军状态<br>running/closed|No|—|
|isTest|bool|是否为测试赛事|No|—|
|leagueGroup|string|优胜冠军联赛群组(EN)|No|—|
|teams|Teams|队伍相关信息|No|—|

#### **Teams**
```
{
	"orid": int,
	"teamId": int,
	"teamName": string,
	"price": decimal,
	"maxBet": int,
	"oddsStatus": string,
	"isUpdate": bool
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|orid|int|优胜冠军赔率ID|No|—|
|teamId|int|队伍ID|No|—|
|teamName|string|队伍名称|No|—|
|price|decimal|赔率 (欧洲盘)|No|—|
|maxBet|int|最大投注额.|No|—|
|oddsStatus|string|盘口状态<br>running/closed|No|—|
|isUpdate|bool|赔率使否异动|No|—|
