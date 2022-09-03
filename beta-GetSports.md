此API用于获取每个运动项目的赛事数量及串关赛事数量 

## Request
```http request
GET  /sports/{version}/GetSports?until=2021-02-28&language=cs
Accept: application/json
Accept-Encoding: br, gzip, deflate
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```

| Parameter | Description |
| ------ | ------ |
| query | 使用Odata指定特定格式的查询 |
| from | 指定赛事开始日期，可以单独输入 |
| until | 指定赛事结束日期，可以单独输入 |
| language | 指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |

## Response
```
{    
    "sports": Sport[]   
} 
```
| Name| Format | Description |
| ------ | ------ | ------ |
| sports | Sport array| sport讯息列表 |

### **Sport**
```
{  
    "sportType": int,  
    "sportName": string,  
    "liveGameCount": int,
    "gameCount": int,
    "parlayGame": int,
    "outrightGame": int
} 
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
| sportType | int | 体育项目ID | Yes | $filter=sporttype eq 1 |
| sportName | string | 体育项目名称 | Yes | $filter=sportname eq 'Soccer' |
| liveGameCount|int|该体育项目的滚球赛事数量|Yes|$filter=liveGameCount gt 0|
| gameCount | int | 该体育项目的非滚球赛事数量 | No | — |
| parlayGame | int | 该体育项目的串关赛事数量 | No | — |
| outrightGame  | int | 该体育项目的优胜冠军赛事数量 | No | — |

