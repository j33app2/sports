此API用于获取赛事结果等相关信息

## **Request**
```http request
GET /betting/{version}/GetGameDetails?eventids=12345,6789
Content-Type: application/json
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```

| Parameter | Format | Length | Mandatory | Description |
| ------ | ------ | ------ | ------ | ------ |
| eventIds | string | 5100 | Yes |赛事ID<br>使用 "*,*" 区隔赛事ID |
| language | string |  | |指定欲回应的数据语系，预设 "**en**"<br>请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |

## **Response**
```
{
    "games": [
        {
            "eventId": string,
            "gameDetail": null
        },
        {
            "eventId": string,
            "gameDetail": {
                "eventTime": DateTime,
                "sportType": int,
                "leagueId": int,
                "leagueName": string,
                "homeId": int,
                "homeName": string,
                "awayId": int,
                "awayName": string,
                "homeScore": int,
                "awayScore": int,
                "htHomeScore": int,
                "htAwayScore": int,
                "gameStatus": string,
                "winItem": string?,
                "cornerSequence": string?
            }
        }
    ]
}
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
|games| Array | 赛事信息列表|


| Parameter | Format | Description |
| ------ | ------ | ------ |
|eventId|string|赛事ID|
|gameDetail|Object?|找不到赛事回应null|


| Parameter | Format | Description |
| ------ | ------ | ------ |
|eventTime|DateTime|开赛时间 (时区GMT+0)|
|sportType|int|体育项目ID|
|leagueId|int|联赛ID|
|leagueName|string|联赛名称|
|homeId|int|主队ID|
|homeName|string|主队名称|
|awayId|int|客队ID|
|awayName|string|客队名称|
|homeScore|int|主队终场得分<br>在高尔夫球赛事中, 'homeScore' 和 'awayScore' 这两个字段为杆数; 若为独赢&获胜者的高尔夫球赛事，数字大者为输。|
|awayScore|int|客队终场得分<br>在高尔夫球赛事中, 'homeScore' 和 'awayScore' 这两个字段为杆数; 若为独赢&获胜者的高尔夫球赛事，数字大者为输。|
|htHomeScore|int|主队半场得分|
|htAwayScore|int|客队半场得分|
|gameStatus|string|赛事状态: <br>**running**: 赛事尚未开始或正在进行中<br>**closed**: 赛事在未开赛前即关闭<br>**postponed**: 赛事延赛<br>**completed**: 赛事已结算<br>**refund**: 赛事取消|
|winItem|string?|主客队终场得分<br>适用 冰上曲棍球(4) /网球(5) /排球(6) /棒球(8) /羽毛球(9) /泰拳(44)|
|cornerSequence|string?|角球进球顺序|
