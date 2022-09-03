```
[
   {
      eventId, 
      eventStatus,
      globalShowTime,
      hasLiveMarket,
      marketCount,
      marketCategories,
      gameInfo: {
          livePeriod,
          seconds,
          isNeutral,
          isHt,
          isBreak,
          isClosed,
          inJuryTime,
          gameStatus,
          inPlayTime,
          delayLive,
          liveHomeScore,
          liveAwayScore
      },
      soccerInfo: {
           homeRedCard,
           awayRedCard,
           homeYellowCard,
           awayYellowCard
       },
      tennisInfo: {
           homeGameScore,
           awayGameScore,
           homePointScore,
           awayPointScore,
           currentSet,
           currentServe
       },
       BeachVolleyBallInfo:{
           homeGameScore,
           awayGameScore,
           currentSet,
           currentServe,
           playerInjury,
           isRain,
       },
       eSportInfo:{
           bestOfMap,
	   isStartingSoon,
	   moveBO3Down,
	   overTimeSession,
	   leagueGroup,
	   leagueGroupId
       },
       basketballInfo:{
	   homeGameScore,
	   awayGameScore,
	   latestLivePeriod,
	   homeOverTimeScore,
	   awayOverTimeScore
       },
       baseballInfo:{
           homeGameScore,
	   awayGameScore,
	   homeOverTimeScore,
	   awayOverTimeScore,
	   baseHasRunner,
           currentInning,
           currentBattingTeam,
           currentOuts
       },
       volleyballInfo:{
           homeGameScore,
	   awayGameScore,
	   homePointScore,
	   awayPointScore,
	   currentServe, 
	   homeCurrentPoint,
	   awayCurrentPoint,
	   playerInjury,
           lastestLivePeriod
       }
   }
]
```

| Name| Format | Description |
| ------ | ------ | ------ |
|eventId|int|赛事ID|
|eventStatus|string|赛事状态<br>running/ closed/ postponed/ deleted|
|globalShowTime|DateTime|开赛时间 (时区**GMT+0**)|
|hasLiveMarket|bool|是否有滚球盘口|
|marketCount|int|该赛事的所有盘口数量|
|marketCategories|int[]|该赛事的所有盘口投注类型<br>0: None (主要) <br>1: FullTime (全场) <br>2: Half (半场) <br>3: Corners (角球)/Bookings (罚牌) <br>4: Intervals (区间) <br>5: Specials (特别产品) <br>6: Players (选手) <br>7: FastMarket (快速盘口) <br>8: Quarter (节) <br>9: ExtraTime (加时) <br>10: Penalty (点球) <br>11-19: E-Sports Map 1-9 (电子竞技适用 – 地图 1~9)|
|gameInfo|GameInfo|球赛相关信息|
|soccerInfo|SoccerInfo|足球相关信息|
|tennisInfo|TennisInfo|网球相关信息|
|BeachVolleyBallInfo|BeachVolleyBallInfo|沙滩排球相关信息|
|eSportInfo|ESportInfo|电子竞技相关信息|
|basketballInfo|BasketballInfo|篮球相关信息|
|baseballInfo|BaseballInfo|棒球相关信息|
|volleyballInfo|VolleyballInfo|排球相关信息|
#### GameInfo

| Name| Format | Description |
| ------ | ------ | ------ |
|livePeriod|byte|目前进行到第几节<br>如果值为 0，则前端不显示时间。这意味着比赛正处于特殊时期。|
|seconds|int|当前赛事时间以秒为单位|
|isNeutral|bool|是否为中立场|
|isHt|bool|是否为中场休息|
|isBreak|bool|赛事是否中断(休息时间)|
|isClosed|bool|赛事是否关闭|
|inJuryTime|byte|伤停时间|
|delayLive|bool|赛事是否延迟|
|gameStatus|byte|球赛状态<br>1=PRC(有可能被判红牌) <br>2=PPen(有可能被判点球) <br>3=VAR(视频助理裁判) <br>4=Penalty(点球) <br>5=Injury(球员受伤) <br>6=Sudden Death(骤死赛)|
|inPlayTime|string|目前赛事时间|
|liveHomeScore|int|主队滚球分数|
|liveAwayScore|int|客队滚球分数|

#### SoccerInfo

| Name| Format | Description |
| ------ | ------ | ------ |
|homeRedCard|byte|主场红牌数|
|awayRedCard|byte|客场红牌数|
|homeYellowCard|byte|主场黄牌数|
|awayYellowCard|byte|客场黄牌数|

#### TennisInfo

| Name| Format | Description |
| ------ | ------ | ------ |
|homeGameScore|int[]|主队每盘获得局数|
|awayGameScore|int[]|客队每盘获得局数|
|homePointScore|string|主队目前局数比分|
|awayPointScore|string|客队目前局数比分|
|currentSet|int|目前盘数|
|currentServe|int|目前发球方|

#### BeachVolleyBallInfo

| Name| Format | Description |
| ------ | ------ | ------ |
|homeGameScore|int[]|主队每盘获得局数|
|awayGameScore|int[]|客队每盘获得局数|
|currentSet|int|目前盘数|
|currentServe|int|目前发球方|
|playerInjury|int|哪支队伍有人受伤<br>0=no one(无), 1=home(主队), 2=away(客队), 3=both(两队) |
|isRain|bool|是否为雨天|

#### ESportInfo

| Name| Format | Description |
| ------ | ------ | ------ |
|bestOfMap|int|Specifies how many maps will be use.|No|—|
|isStartingSoon|bool|Specifies the competition is starting soon.|No|—|
|moveBO3Down|bool|Specifies to display a flag in web page.|No|—|
|overTimeSession|int|<p>Specifies the information of league.<br>1 → Dota2 ; 2 → LOL ; 3 → CS2 ; 4 → KOG ; 99 → Others</p>|Yes|$filter=overTimeSession eq 1|
|leagueGroup|string|Specifies the name of the league group.|No|—|
|leagueGroupId|int|Specifies the identifier of the league group.|No|—|

#### **BasketballInfo**

| Name| Format | Description |
| ------ | ------ | ------ |
|homeGameScore|int[]|主队目前得分|
|awayGameScore|int[]|客队目前得分|
|latestLivePeriod|int|目前进行节数|
|homeOverTimeScore|int|主隊延長賽得分|
|awayOverTimeScore|int|客队延长赛得分|

#### **BaseballInfo**

| Name| Format | Description |
| ------ | ------ | ------ |
|homeGameScore|int[]|主队目前得分|
|awayGameScore|int[]|客队目前得分|
|homeOverTimeScore|int|主隊延長賽比分|
|awayOverTimeScore|int|客队延长赛比分|
|baseHasRunner|bool[]|垒上是否有跑者<br>第一笔项目为一垒是否有跑者，二、三垒以此类推|
|currentInning|int|目前局数|
|currentBattingTeam|int|目前打击队伍<br>1=主队，2=客队|
|currentOuts|int|目前出局数|

#### **VolleyballInfo**

| Name| Format | Description |
| ------ | ------ | ------ |
|homeGameScore|int[]|主队每盘获得局数|
|awayGameScore|int[]|客队每盘获得局数|
|homePointScore|int|主队目前总比分|
|awayPointScore|int|客队目前总比分|
|currentServe|int|目前发球方|
|homeCurrentPoint|int|主队目前比分|
|awayCurrentPoint|int|客队目前比分|
|playerInjury|int|哪支队伍有人受伤<br>0=no one(无), 1=home(主队), 2=away(客队), 3=both(两队) |
|latestLivePeriod|int|目前进行的节数|