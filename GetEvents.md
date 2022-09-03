此API用于获取赛事相关信息包含部分盘口信息

## Request
```http request
GET  /sports/{version}/GetEvents?query=$filter=sporttype eq 1&includeMarkets=$filter=bettype eq 128&language=cs
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
| includeMarkets | 此参数仅在 **/GetEvents** 中使用，指定是否有必要回传market讯息。<br>**如果includeMarkets未指定，则默认回传。** <br /> **includeMarkets = $filter=bettype eq 128;** 仅筛选指定条件Market信息。<br> **includeMarkets = none;** 将不回传Market信息。|

## Response
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
        "leagueIconUrl": string,
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
	"isCashout": bool,
	"isVirtualEvent": bool,
	"hasLiveMarket": bool,
	"marketCount": int,
	"marketCategories": int[],
	"streamingOption ": int,
	"channelCode ": string,
	"teamInfo": TeamInfo,
	"gameInfo": GameInfo,
	"soccerInfo": SoccerInfo | null,
	"tennisInfo": TennisInfo | null,
	"beachVolleyBallInfo": BeachVolleyBallInfo | null,
	"eSportInfo": ESportInfo | null,
        "basketballInfo": BasketballInfo | null,
        "baseballInfo": BaseballInfo | null,
        "volleyBallInfo": VolleyballInfo | null
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|sportType|int|体育项目ID|Yes|$filter=sporttype eq 1|
|sportName|string|体育项目名称|Yes|$filter=sportname eq 'Soccer'|
|leagueId|int|联赛ID|Yes|$filter=leagueid eq 56038|
|leagueName|string|联赛名称|Yes|$filter=leaguename eq '*UEFA CHAMPIONS LEAGUE'  or $filter=contains(leaguename,'NBA')|
|leagueIconUrl|string|联赛图片URL, 如果图片不存在请使用预设联赛图片URL<br>{domain}/LeagueImg/league_flag.png<br>domain请用leagueIconUrl返回的domain取代|No|-|
|eventId|int|赛事ID|Yes|$filter=eventid eq 38255274|
|eventCode|string|赛事代码|No|—|
|eventStatus|string|赛事状态<br>running/ closed/ postponed/ deleted|Yes|$filter=eventStatus eq 'running'|
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
|marketCategories|int[]|该赛事的所有盘口投注类型<br>0: None (主要) <br>1: FullTime (全场) <br>2: Half (半场) <br>3: Corners (角球)/Bookings (罚牌) <br>4: Intervals (区间) <br>5: Specials (特别产品) <br>6: Players (选手) <br>7: FastMarket (快速盘口) <br>8: Quarter (节) <br>9: ExtraTime (加时) <br>10: Penalty (点球) <br>11-19: E-Sports Map 1-9 (电子竞技适用 – 地图 1~9)|No|—|
|streamingOption|int|视频ID |Yes|$filter=streamingOption eq 131072|
|channelCode|string|视频代码|Yes|$filter=channelCode ne null|
|teamInfo|TeamInfo|团队相关信息|No|—|
|gameInfo|GameInfo|球赛相关信息|No|—|
|soccerInfo|SoccerInfo|足球相关信息|No|—|
|tennisInfo|TennisInfo|网球相关信息|No|—|
|beachVolleyBallInfo|BeachVolleyBallInfo|沙滩排球相关信息|No|—|
|eSportInfo|ESportInfo|电子竞技相关信息|No|—|
|basketballInfo|BasketballInfo|篮球相关信息|No|—|
|baseballInfo|BaseballInfo|棒球相关信息|No|—|
|volleyballInfo|VolleyballInfo|排球相关信息|No|—|
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
|homeIconUrl|string|主队队徽URL, 如果图片不存在请使用预设主队队徽URL<br>{domain}/TeamImg/team_flag_home.png<br>domain请用homeIconUrl返回的domain取代|No|-|
|awayId|int|客队ID|Yes|$filter=awayid eq 714227|
|awayName|string|客队名称 |Yes|$filter=contains(awayname,'Lakers')|
|awayIconUrl|string|客队队徽URL, 如果图片不存在请使用预设客队队徽URL<br>{domain}/TeamImg/team_flag_away.png<br>domain请用homeIconUrl返回的domain取代|No|-|

#### **GameInfo**
```
{
	"livePeriod": byte,
	"clockDirection": string,
	"seconds": int,
	"isNeutral": bool,
	"isHt": bool,
	"isBreak": bool,
	"isClosed": bool,
	"inJuryTime": byte,
	"delayLive": bool,
	"gameStatus" byte,
	"inPlayTime": string,
	"liveHomeScore": int,
	"liveAwayScore": int
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|livePeriod|byte|目前进行到第几节<br>如果值为 0，则前端不显示时间。这意味着比赛正处于特殊时期。<br>仅支援以下运动类型:<br>1: 足球 <br>2: 篮球 <br>3: 美式足球 <br>4: 冰上曲棍球<br>9: 羽毛球<br>24: 手球<br>26: 橄榄球<br>43: 电子竞技|No|—|
|clockDirection|string|赛事时间计算方式<br>inc：从0开始计数到赛事结束<br> dec：从特定值开始计数到0|No|—|
|seconds|int|当前赛事时间以秒为单位|No|—|
|isNeutral|bool|是否为中立场|No|—|
|isHt|bool|是否为中场休息|No|—|
|isBreak|bool|赛事是否中断(休息时间)|No|—|
|isClosed|bool|赛事是否关闭|No|—|
|inJuryTime|byte|伤停时间|No|—|
|delayLive|bool|赛事是否延迟|No|—|
|gameStatus|byte|球赛状态<br>1=PRC(有可能被判红牌) <br>2=PPen(有可能被判点球) <br>3=VAR(视频助理裁判) <br>4=Penalty(点球) <br>5=Injury(球员受伤) <br>6=Sudden Death(骤死赛) |No|—|
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

#### **BeachVolleyBallInfo**
```
{
	"homeGameScore": int[],
	"awayGameScore": int[],
	"currentSet": int,
	"currentServe": int,
	"playerInjury": int,
	"isRain" bool`
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|homeGameScore|int[]|主队每盘获得局数|No|—|
|awayGameScore|int[]|客队每盘获得局数|No|—|
|currentSet|int|目前盘数|No|—|
|currentServe|int|目前发球方|No|—|
|playerInjury|int|哪支队伍有人受伤<br>0=no one(无), 1=home(主队), 2=away(客队), 3=both(两队) |No|—|
|isRain|bool|是否为雨天|No|—|

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
|isStartingSoon|bool|是否即将开赛|No|—|
|moveBO3Down|bool|控制是否显示网页的旗帜 |No|—|
|overTimeSession|int|联赛信息<br>1 → Dota2 ; 2 → LOL ; 3 → CS2 ; 4 → KOG ; 99 → Others|Yes|$filter=overTimeSession eq 1|
|leagueGroup|string|电子竞技联赛名称|No|—|
|leagueGroupId|int|电子竞技联赛ID|No|—|
#### **BasketballInfo**
```
{
	"homeGameScore": int[],
	"awayGameScore": int[],
	"latestLivePeriod":int,
	"homeOverTimeScore": int,
	"awayOverTimeScore": int
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|homeGameScore|int[]|主队目前得分|No|—|
|awayGameScore|int[]|客队目前得分|No|—|
|latestLivePeriod|int|目前进行节数|No|—|
|homeOverTimeScore|int|主隊延長賽得分|No|—|
|awayOverTimeScore|int|客队延长赛得分|No|—|
#### **BaseballInfo**
```
{
	"homeGameScore": int[],
	"awayGameScore": int[],
	"homeOverTimeScore": int,
	"awayOverTimeScore": int,
	"baseHasRunner": bool[],
        "currentInning": int,
        "currentBattingTeam": int,
        "currentOuts": int
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|homeGameScore|int[]|主队目前得分|No|—|
|awayGameScore|int[]|客队目前得分|No|—|
|homeOverTimeScore|int|主隊延長賽比分|No|—|
|awayOverTimeScore|int|客队延长赛比分|No|—|
|baseHasRunner|bool[]|垒上是否有跑者<br>第一笔项目为一垒是否有跑者，二、三垒以此类推|No|—|
|currentInning|int|目前局数|No|—|
|currentBattingTeam|int|目前打击队伍<br>1=主队，2=客队|No|—|
|currentOuts|int|目前出局数|No|—|
#### **VolleyballInfo**
```
{
	"homeGameScore": int[],
	"awayGameScore": int[],
	"homePointScore":int,
	"awayPointScore":int,
	"currentServe":int, 
	"homeCurrentPoint":int,
	"awayCurrentPoint":int,
	"playerInjury":int,
        "lastestLivePeriod":int
}
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|homeGameScore|int[]|主队每盘获得局数|No|—|
|awayGameScore|int[]|客队每盘获得局数|No|—|
|homePointScore|int|主队目前总比分|No|—|
|awayPointScore|int|客队目前总比分|No|—|
|currentServe|int|目前发球方|No|—|
|homeCurrentPoint|int|主队目前比分|No|—|
|awayCurrentPoint|int|客队目前比分|No|—|
|playerInjury|int|哪支队伍有人受伤<br>0=no one(无), 1=home(主队), 2=away(客队), 3=both(两队) |No|—|
|latestLivePeriod|int|目前进行的节数|No|—|

### **Market**
盘口相关信息请参阅[GetMarkets]( /j33app2/sports/wiki/GetMarkets)
