此API用于获取盘口相关信息

## Request
```http request
GET  /sports/{version}/GetMarkets?query=$filter=eventId eq 38255274 and bettype eq 127&language=cs
Accept: application/json
Accept-Encoding: br, gzip, deflate
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```

| Parameter | Description |
| ------ | ------ |
| query | 使用Odata指定特定格式的查询|
| language | 指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |
## Response
```
{    
    "markets": Market[]   
} 
```
| Name| Format | Description |
| ------ | ------ | ------ |
| markets | array| 盘口信息列表 |

### **Market**
```
{
    "sportType": int,
    "eventId": int,
    "betType": int,
    "betTypeName": string,
    "marketId": int,
    "maxBet": decimal,
    "isLive": bool,
    "marketStatus": string,
    "gameMap": short?,
    "gameRound": short?,
    "resourceId": string,
    "category": int,
    "sort": int,
    "combo": int,
    "selections": SelectionInfo[]
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|sportType|int|体育项目ID|Yes|$filter=sporttype eq 1|
|eventId|int|赛事ID|Yes|$filter=eventid eq 38255274|
|betType|int|投注类型|Yes|$filter=bettype eq 128|
|betTypeName|string|投注类型名称|No|—|
|marketId|int|盘口ID|Yes|$filter=marketed eq 274175476|
|maxBet|decimal|最大投注限额|No|—|
|isLive|bool|是否为滚球赛事|Yes|$filter=islive eq true|
|marketStatus|string|盘口状态<br>running / suspend / closePrice / closed|Yes|$filter=marketStatus eq 'running'|
|gameMap|short?|[电子竞技专用]游戏地图<br>当体育项目sport type = 43 且投注类型bettype于9001-9100之间 |No|—|
|gameRound|short?|[电子竞技专用] 游戏回合<br>当体育项目sport type = 43 且投注类型bettype = 9007, 9011, 9027, 9062, 9068, 9070, 9071, 9072, 9073, 9077|No|—|
|resourceId|string|资源 ID |No|—|
|category|int|投注类型分类<br>0: None (主要) <br>1: FullTime (全场) <br>2: Half (半场) <br>3: Corners (角球)/Bookings (罚牌) <br>4: Intervals (区间) <br>5: Specials (特别产品) <br>6: Players (选手) <br>7: FastMarket (快速盘口) <br>8: Quarter (节) <br>9: ExtraTime (加时) <br>10: Penalty (点球) <br>11-19: E-Sports Map 1-9 (电子竞技适用 – 地图 1~9)|Yes|$filter=category eq 0|
|sort|int|排序球头<br>当投注类型bet type=1,3,7,8且有多球头时|Yes|$filter=sort eq 1|
|combo|int|赛事串关数量限制<br>0: 该盘口不支持串关<br>2: 下注时最少需要选2种组合<br>3: 下注时最少需要选3种组合|Yes|$filter=combo ge 2|
|selections|SelectionInfo[]|盘口赔率项目列表|No|—|

#### **SelectionInfo**
```
[
	{
	    "key": string,
	    "keyName": string,
	    "point": decimal?,
	    "point2": decimal?,
	    "oddsPrice": OddsPriceInfo
	}
]
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|key|string|投注类型选项|No|—|
|keyName|string|投注类型选项名称|No|—|
|point|decimal?|球头|No|—|
|point2|decimal?|球头2 <br>Only for bet type=646;<br> point=HDP, point2=OU|No|—|
|oddsPrice|OddsPriceInfo|赔率相关信息|No|—|

##### **OddsPriceInfo**
```
{
	"parlayPrice": decimal,
	"malayPrice": decimal,
	"hongKongPrice": decimal,
	"decimalPrice": decimal,
	"indoPrice": decimal,
	"americanPrice": decimal
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|parlayPrice|decimal|串关赔率|No|—|
|malayPrice|decimal|马来盘赔率|No|—|
|hongKongPrice|decimal|香港盘赔率|No|—|
|decimalPrice|decimal|欧洲盘赔率|No|—|
|indoPrice|decimal|印度尼西亚盘赔率|No|—|
|americanPrice|decimal|美国盘赔率|No|—|
