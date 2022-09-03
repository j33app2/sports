### API端点
- **API Request**  
  https://{domain name}/{category}/{version}/{method}.
- **URL Description**  
  - version：
    API版本号，例如beta或V1或更新的版本
  - category：  
    要使用的API类别，例如sports或betting。  
  - method：  
    要使用的API方法，例如GetEvents。.
    
- **API Response**  
  回应数据为JSON格式。

---
### Http Pull
Odds Direct API可以拉取及更新数据。
以下以/GetEvents示范操作

```http request
GET /Sports/{version}/GetEvents?query=$filter=sporttype eq 1&includeMarkets=$filter=bettype eq 128&language=cs
Accept: application/json
Accept-Encoding: br, gzip, deflate
Authorization: Bearer {JWT token}
```
该结果会以以下方式回应
```
{
"sports": [{...},{...},{...},{...},{...},{...},{...},{...},{...},{...}],
"leagues": [{...},{...},{...},{...},{...},{...},{...},{...},{...},{...}],
"events": [{...},{...},{...},{...},{...},{...},{...},{...},{...},{...}],
"markets": [{...},{...},{...},{...},{...},{...},{...},{...},{...},{...}],
"outrights": [{...},{...},{...},{...},{...},{...},{...},{...},{...},{...}],
}
```

### HTTP parameters
| 参数 | 说明 |
| ------ | ------ |
| query | 使用Odata指定特定格式的查询 |
| from | 指定赛事开始日期，可以单独输入 |
| until | 指定赛事结束日期，可以单独输入 |
| language | 指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |
| includeMarkets | 此参数仅在 **/GetEvents** 中使用，指定是否有必要回传market讯息。<br>**如果includeMarkets未指定，则默认回传。** <br /> **includeMarkets = $filter=bettype eq 128;** 仅筛选指定条件Market信息。<br /> **includeMarkets = none;** 将不回传Market信息。|

