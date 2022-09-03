此API用于获取热门推荐赛事相关信息包含部分盘口信息

## Request
```http request
GET  /sports/{version}/GetPromotions
Accept: application/json
Accept-Encoding: br, gzip, deflate
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```
| Parameter | Description |
| ------ | ------ |
| query | 使用Odata指定特定格式的查询 |
| language | 指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |
| includeMarkets | 指定是否有必要回传market讯息。<br>**如果includeMarkets未指定，则默认回传。** <br /> **includeMarkets = $filter=bettype eq 128;** 仅筛选指定条件Market信息。<br> **includeMarkets = none;** 将不回传Market信息。|

## **Response**
```
{    
    "events": Event[],
    "markets": Market[] | null 
} 
```
| Name| Format | Description |
| ------ | ------ | ------ |
| events | Event array | 赛事信息列表|
| markets | Market array | 盘口信息列表|

### **Event**
```
{
	"sportType": int,
	"sportName": string,
	"leagueId": int,
	"leagueName": string,
	"eventId": int,
	"eventCode": string,
	"eventStatus": string,
	"isMainMarket": bool,
	"kickOffTime": DateTime,
	"globalShowTime": DateTime,
	"countryCode": string,
	"gameSession": int,
	"parentId": int,
	"isTest": bool,
	"isLive": bool,
	"isParlay": bool,
	"isVirtualEvent": bool,
	"hasLiveMarket": bool,
	"marketCount": int,
	"marketCategories": int[],
	"streamingOption ": int,
	"channelCode ": string,
	"teamInfo": TeamInfo,//Described in a separate table blow.
	"gameInfo": GameInfo,//Described in a separate table blow.
	"soccerInfo": SoccerInfo | null,//Described in a separate table blow.
	"tennisInfo": TennisInfo | null,//Described in a separate table blow.
	"eSportInfo": ESportInfo | null,//Described in a separate table blow.
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|sportType|int|体育项目ID|Yes|$filter=sporttype eq 1|
|sportName|string|体育项目名称|Yes|$filter=sportname eq 'Soccer'|
|leagueId|int|联赛ID|Yes|$filter=leagueid eq 56038|
|leagueName|string|联赛名称|Yes|$filter=leaguename eq '*UEFA CHAMPIONS LEAGUE'  or $filter=contains(leaguename,'NBA')|
|eventId|int|赛事ID|Yes|$filter=eventid eq 38255274|
|eventCode|string|赛事代码|No|—|
|eventStatus|string|赛事状态<br>running/closed/postponed/ deleted|No|—|
|isMainMarket|bool|是否为主要盘口|Yes|$filter=ismainmarket eq true |
|kickOffTime|DateTime|系统开赛时间 (时区**GMT+0**)|No|—|
|globalShowTime|DateTime|开赛时间 (时区**GMT+0**)|No|—|
|countryCode|string|联赛国别代码|No|—|
|gameSession|int|赛事比赛有多少节|No|—|
|parentId|int|该赛事的母赛事ID|No|—|
|isTest|bool|是否为测试赛事|No|—|
|isLive|bool|是否为滚球赛事|Yes|$filter=islive eq true|
|isParlay|bool|是否为串关赛事|Yes|$filter=isparlay eq true|
|isCashout|bool|赛事是否支持实时兑现|Yes|$filter=iscashout eq true|
|isVirtualEvent|bool|是否为虚拟赛事|Yes|$filter=isvirtualevent eq true|
|hasLiveMarket|bool|是否有滚球盘口|No|—|
|marketCount|int|该赛事的所有盘口数量|No|—|
|marketCategories|int[]|该赛事的所有盘口投注类型|No|—|
|streamingOption|int|视频ID |No|—|
|channelCode|string|视频代码|No|—|
|teamInfo|TeamInfo|团队相关信息|No|—|
|gameInfo|GameInfo|球赛相关信息|No|—|
|soccerInfo|SoccerInfo|足球相关信息|No|—|
|tennisInfo|TennisInfo|网球相关信息|No|—|
|eSportInfo|ESportInfo|电子竞技相关信息|No|—|

#### **TeamInfo**
```
{
	"homeId": int,
	"homeName": string,
	"homeIconUrl": string
	"awayId": int,
	"awayName": string,
	"awayIconUrl": string
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|homeId|int|主队ID|Yes|$filter=homeId eq 17892|
|homeName|string|主队名称|Yes|$filter=contains(homename,'Field')|
|homeIconUrl|string|主队队徽URL, 如果图片不存在请使用预设主队队徽URL<br>{domain}/TeamImg/team_flag_home.png|No|-|
|awayId|int|客队ID|Yes|$filter=awayid eq 714227|
|awayName|string|客队名称 |Yes|$filter=contains(awayname,'Lakers')|
|awayIconUrl|string|客队队徽URL, 如果图片不存在请使用预设客队队徽URL<br>{domain}/TeamImg/team_flag_away.png|No|-|

#### **GameInfo**
```
{
	"livePeriod": byte,
	"isNeutral": bool,
	"isHt": bool,
	"isBreak": bool,
	"isClosed": bool,
	"inJuryTime": int,
	"delayLive": bool,
	"gameStatus" byte,
	"inPlayTime": string,
	"liveHomeScore": int,
	"liveAwayScore": int
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|livePeriod|byte|目前进行到第几节|No|—|
|isNeutral|bool|是否为中立场|No|—|
|isHt|bool|是否为中场休息|No|—|
|isBreak|bool|赛事是否中断(休息时间)|No|—|
|isClosed|bool|赛事是否关闭|No|—|
|inJuryTime|byte|伤停时间|No|—|
|delayLive|bool|赛事是否延迟|No|—|
|gameStatus|byte|球赛状态<br>1=PRC(有可能被判红牌); <br>2=PPen(有可能被判点球); <br>3=VAR(视频助理裁判); <br>4=Penalty(点球); <br>5=Injury(球员受伤); <br>6=Sudden Death(骤死赛) |No|—|
|inPlayTime|string|目前赛事时间|No|—|
|liveHomeScore|int|主队滚球分数|No|—|
|liveAwayScore|int|客队滚球分数 |No|—|

#### **SoccerInfo**
```
{
	"homeRedCard":byte,
	"awayRedCard":byte,
	"homeYellowCard":byte,
	"awayYellowCard":byte
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|homeRedCard|byte|主场红牌数|No|—|
|awayRedCard|byte|客场红牌数|No|—|
|homeYellowCard|byte|主场黄牌数|No|—|
|awayYellowCard|byte|客场黄牌数|No|—|

#### **TennisInfo**
```
{
	"homeGameScore": int[],
	"awayGameScore": int[],
	"homePointScore": string,
	"awayPointScore": string,
	"currentSet": int,
	"currentServe": int
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|homeGameScore|int[]|主队每盘获得局数|No|—|
|awayGameScore|int[]|客队每盘获得局数|No|—|
|homePointScore|string|主队目前局数比分|No|—|
|awayPointScore|string|客队目前局数比分|No|—|
|currentSet|int|目前盘数|No|—|
|currentServe|int|目前发球方|No|—|

#### **ESportInfo**
```
{
	"bestOfMap": int,
	"isStartingSoon": bool,
	"moveBO3Down": bool,
	"overTimeSession": int,
	"leagueGroup": string,
	"leagueGroupId": int
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|bestOfMap|int|Best Of Map标识会打几个地图|No|—|
|isStartingSoon|bool|S是否即将开赛|No|—|
|moveBO3Down|bool|控制是否显示网页的旗帜 |No|—|
|overTimeSession|int|联赛信息<br>1 → Dota2 ; 2 → LOL ; 3 → CS2 ; 4 → KOG ; 99 → Others|No|—|
|leagueGroup|string|电子竞技联赛名称|No|—|
|leagueGroupId|int|电子竞技联赛ID|No|—|

### **Market**
```
{
    "sportType": int,
	"eventId": int,
	"betType": int,
	"betTypeName": string,
	"sportType": int,
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
|marketStatus|string|盘口状态<br>running / suspend / closePrice / closed|No|—|
|gameMap|short?|[电子竞技专用]游戏地图<br>when sport type = 43 and bet type in 9001-9100 |No|—|
|gameRound|short?|[电子竞技专用] 游戏回合<br>when sport type = 43 and bet type = 9007, 9011, 9027, 9062, 9068, 9070, 9071, 9072, 9073, 9077|No|—|
|resourceId|string|资源 ID |No|—|
|category|int|投注类型分类<br>0: None (主要) ; <br>1: FullTime (全场) ; <br>2: Half (半场) ; <br>3: Corners (角球) ; <br>4: Bookings (罚牌) ; <br>5: Intervals (区间) ; <br>6: Specials (特别产品) ; <br>7: Players (选手) ; <br>8: ExtraTime (加时) ; <br>9: FastMarket (快速盘口) ; <br>10: Quarter (节) ; <br>11-19: E-Sports Map 1-9|No|—|
|sort|int|排序<br>when bet type=1,3,7,8 and have multiple point.|No|—|
|combo|int|赛事串关限制|No|—|
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
