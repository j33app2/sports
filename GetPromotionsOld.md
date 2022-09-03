此API用于获取热门推荐赛事相关信息包含部分盘口信息

## Request
```http request
GET  /sports/{version}/GetPromotions?OddsType=1&Language=cs
Accept: application/json
Authorization: Bearer {JWT token}
```

| Parameter | Description |
| ------ | ------ |
| OddsType | 盘口赔率类型<br> 1 : Malay Odds ; 2 : Hong Kong Odds ; 3 : Decimal Odds ; 4 : Indo Odds ; 5 : American Odds|
| Language | 指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |

## **Response**
```
{    
    "events": Event[],
    "markets": Market[]  
} 
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
|events|Event array|赛事信息列表|
|markets|Market array|盘口信息列表|

### **Event**
```
{
    "sportType": int,
    "sportName": string,
    "eventId": int,
    "leagueId": int,
    "leagueName": string,
    "globalShowTime": DateTime,
    "isLive": false,
    "inPlayTime": string,
    "homeId": int,
    "homeName": string,
    "homeIconUrl": string,
    "liveHomeScore": int,
    "awayId": int,
    "awayName": string,
    "awayIconUrl": string,
    "liveAwayScore": int
}
```
| Name| Format | Description |
| ------ | ------ | ------ |
|sportType|int|体育项目 ID|
|sportName|string|体育项目名称|
|eventId|int|赛事ID|
|leagueId|int |联赛ID|
|leagueName|string|联赛名称|
|globalShowTime|DateTime|开赛时间 (时区**GMT+0**)|
|isLive|bool|是否为滚球赛事|
|homeId|int|主队ID|
|homeName|string|主队名称|
|homeIconUrl|string|主队队徽URL|
|liveHomeScore|int|主队滚球分数|
|awayId|int|客队ID|
|awayName|string|客队名称|
|awayIconUrl|string|客队队徽URL|
|liveAwayScore|int|客队滚球分数|

### **Markets**
```
{
    "eventId": int,
    "marketId": int,
    "betType": int,
    "betTypeName": string,
    "selections": SelectionInfo[]
}
```
| Name| Format | Description |
| ------ | ------ | ------ |
|eventId|int|赛事ID|
|marketId|int|盘口ID|
|betType|int|投注类型|
|betTypeName|string|投注类型名称|
|selections|SelectionInfo[]|赔率相关信息|

#### **SelectionInfo**
```
{
    "key": string,
    "keyName": string,
    "point": decimal,
    "point2": decimal?,
    "price": decimal
}
```
| Name| Format | Description |
| ------ | ------ | ------ |
|key|string|投注类型选项|
|keyName|string|投注类型选项名称|
|point|decimal|球头|
|point2|decimal?|球头2<br>Only for bet type=646;<br> point=HDP, point2=OU|
|price|decimal|赔率|
