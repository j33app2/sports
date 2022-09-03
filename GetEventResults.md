此 API 用于获取指定时间区间内运动的赛果信息。
* 仅支持查询最近 12 天内的结果。

## Request
```http request
GET  /sports/{version}/GetEventResults?from=2022-01-01&until=2022-01-02&language=cs
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
            "countryCode": string, 
            "eSportGroup": int?, 
            "gameSession": int, 
            "isTest": bool, 
            "events": [ 
                { 
                    "eventId": int, 
                    "homeId": int, 
                    "homeName": string, 
                    "awayId": int, 
                    "awayName": string, 
                    "htHomeScore": string, 
                    "htAwayScore": string, 
                    "homeScore": string, 
                    "awayScore": string, 
                    "firstHomeScore": string, 
                    "firstAwayScore": string, 
                    "secondHomeScore": string, 
                    "secondAwayScore": string, 
                    "homeGameScore": string, 
                    "awayGameScore": string, 
                    "sessionScores": [ 
                        { 
                            "homeScore": string, 
                            "awayScore": string, 
                            "isRefund": bool 
                        } 
                    ], 
                    "overTimeScores": [ 
                        { 
                            "homeScore": string, 
                            "awayScore": string, 
                            "isRefund": bool 
                        } 
                    ], 
                    "gameStatus": string, 
                    "winDetail": string 
                    "eventTime": dateTime, 
                    "soccerDetail": { 
                        "firstGoal": string, 
                        "lastGoal": string, 
                        "firstHtGoal": string, 
                        "lastHtGoal": string, 
                        "goalSequence": string, 
                        "cornerSequence": string, 
                        "penaltySequence": string, 
                        "firstGoalMethod": string, 
                        "firstGoalScorerPlayer": string, 
                        "specialData": [ 
                            { 
                                "leagueId": int, 
                                "leagueName": string, 
                                "eventId": int,
                                "homeId": int, 
                                "homeName": string, 
                                "awayId": int, 
                                "awayName": string, 
                                "htHomeScore": string, 
                                "htAwayScore": string, 
                                "homeScore": string, 
                                "awayScore": string, 
                                "sort": int, 
                                "status": string 
                            } 
                        ],
                        "deathSuddenPenaltySequence": string,
                        "isPenaltyHandicap": bool,
                        "isPenaltyOverUnder": bool
                    }, 
                    "eSportDetail": { 
                        "maps": [ 
                            { 
                                "map": int, 
                                "homeScore": string 
                                "awayScore": string 
                                "status": string 
                            } 
                        ] 
                    } 
                } 
            ] 
        } 
    ] 
} 
```
| Parameter | Format | Description | 
| ------ | ------ | ------ | 
| result | Object Array| 赛果信息列表|

### Result Object
| Parameter | Format | Description | Queryable |  Query Example |
| ------ | ------ | ------ | ------ | ------ |
|sportType |int|体育项目ID|Yes|$filter=sporttype eq 1|
|sportName |string|体育项目名称|Yes|$filter=sportname eq 'Soccer' |
|leagueId |int|联赛ID|Yes|$filter=leagueid eq 56038 |
|leagueName |string|联赛名称|Yes|$filter=leaguename eq '*UEFA CHAMPIONS LEAGUE' or $filter=contains(leaguename,'NBA') |
|countryCode|string|联赛国别代码|No| — |
|eSportGroup|int?|电子竞技群组<br>请参阅[E-Sports Group Enumeration](/j33app2/sports/wiki/E-Sports-Group-Enumeration) |No| — |
|gameSession|int|赛事比赛有多少节|No| — |
|isTest|bool|是否为测试赛事|No| — |
|events|Object Array|赛事赛果信息列表|No| — |

#### Events Object
| Parameter | Format | Description | Queryable |  Query Example |
| ------ | ------ | ------ | ------ | ------ |
|eventId|int|赛事ID|Yes| $filter=eventid eq 38255274 |
|homeId|int|主队ID|Yes| $filter=homeId eq 17892 |
|homeName|string|主队名称|Yes| $filter=contains(homename,'Field') |
|awayId|int|客队ID|Yes| $filter=awayid eq 714227 |
|awayName|string|客队名称|Yes| $filter=contains(awayname,'Lakers') |
|htHomeScore|string|主队半场得分|No| — |
|htAwayScore|string|客队半场得分|No| — |
|homeScore|string|主队终场得分|No| — |
|awayScore|string|客队终场得分|No| — |
|firstHomeScore|string|主队第一局的得分 <br> 仅适用 板球(50)|No| — |
|firstAwayScore|string|客队第一局的得分 <br> 仅适用 板球(50)|No| — |
|secondHomeScore|string|主队第二局的得分 <br> 仅适用 板球(50) |No| — |
|secondAwayScore|string|客队第二局的得分 <br> 仅适用 板球(50)|No| — |
|homeGameScore|string|主隊的總比賽得分 <br>适用 网球(5),排球(6),羽毛球(9),壁球(30),沙滩排球(45),藤球(48) |No| — |
|awayGameScore|string|客队的總比賽得分 <br>适用 网球(5),排球(6),羽毛球(9),壁球(30),沙滩排球(45),藤球(48) |No| — |
|sessionScores|Object Array|各节的详细信息|No| — |
|overTimeScores|Object Array|各加时賽的详细信息 |No| — |
|gameStatus|string|赛事状态<br>Running(进行中),Completed(已完场),Refund FT(退款(全场)),Refund HT(退款(半场)),Refund(退款),Pending(延期),Abandoned 1H(在上半场中止),Abandoned 2H(在下半场中止),Under Settlement(结算中),Result Pending(赛果待定)|No| — |
|winDetail|string|获胜方法的详细信息<br>仅适用 泰拳(44) |No| — |
|eventTime|DateTime|赛事时间 (时区GMT+0)|No| — |
|soccerDetail| SoccerDetail Array|足球赛果详细信息 |No| — |
|eSportDetail| ESportDetail Array|电子竞技赛果详细信息|No| — |

### SessionScores / OverTimeScores
| Parameter | Format | Description | Queryable |  Query Example |
| ------ | ------ | ------ | ------ | ------ |  
|homeScore|string| 主队各节的得分|No| — |
|awayScore|string| 客队各节的得分|No| — |
|isRefund|string| 此节是否需退款|No| — |

### SoccerDetail
| Parameter | Format | Description | Queryable |  Query Example | 
| ------ | ------ | ------ | ------ | ------ |  
|firstGoal|string|哪支球队在全场比赛中获得第一个进球<br>将返回"h"、"a"或 null |No| — |
|lastGoal|string|哪支球队在全场比赛中获得最后一个进球<br>将返回"h"、"a"或 null  |No| — |
|firstHtGoal|string|哪支球队在上半场获得第一个进球<br>将返回"h"、"a"或 null  |No| — |
|lastHtGoal|string|哪支球队在上半场获得最后一个进球<br>将返回"h"、"a"或 null  |No| — |
|goalSequence|string| 进球顺序|No| — |
|cornerSequence|string|角球进球顺序 |No| — |
|penaltySequence|string|点球进球顺序|No| — |
|firstGoalMethod|string|第一个进球的方法<br>Shot(射门), Header(头球), Penalty(点球), Free Kick(任意球), Own Goal(乌龙球), No Goal(无进球) |No| — |
|specialData|Object Array|球赛事的特殊信息 |No| — |
|deathSuddenPenaltySequence|string|骤死赛点球进球顺序|No| — |
|isPenaltyHandicap|bool|此赛事是否为点球让分盘赛果|No| — |
|isPenaltyOverUnder|bool|此赛事是否为点球大小盘赛果|No| — |

[comment]: <> (|firstGoalScorerPlayer|string|Specifies the player who gets the first goal. |No| — |)

#### SpecialData
| Parameter | Format | Description | Queryable |  Query Example |
| ------ | ------ | ------ | ------ | ------ |  
|leagueId|int|联赛ID|No| — |
|leagueName|string|联赛名称|No| — |
|eventId|int|赛事ID|No| — |
|homeId|int|主队ID|No| — |
|homeName|string|主队名称|No| — |
|awayId|int|客队ID|No| — |
|awayName|string|客队名称|No| — |
|htHomeScore|string|主队半场得分|No| — |
|htAwayScore|string|客队半场得分 |No| — |
|homeScore|string|主队得分|No| — |
|awayScore|string|客队得分|No| — |
|sort|int|排序|No| — |
|status|string|赛事状态<br>Running(进行中),Completed(已完场),Refund FT(退款(全场)),Refund HT(退款(半场)),Refund(退款),Pending(延期),Abandoned 1H(在上半场中止),Abandoned 2H(在下半场中止),Under Settlement(结算中),Result Pending(赛果待定)|No| — |

### ESportDetail
| Parameter | Format | Description | Queryable |  Query Example | 
| ------ | ------ | ------ | ------ | ------ |
|maps|Object Array| 电子竞技各地图的详细信息|No| — |
#### Maps
| Parameter | Format | Description | Queryable |  Query Example |
| ------ | ------ | ------ | ------ | ------ |  
|map|int| 游戏地图|No| — |
|homeScore|string|主队得分 |No| — |
|awayScore|string|客队得分|No| — |
|status|string|赛事状态 <br>Refund FT(退款(全场)), Refund HT(退款(半场)), Refund(退款), Completed(已完场)|No| — |
