此API用于获取优胜冠军赛事信息。
* 通过此API在一个请求中订阅更新和检索数据。

## Request
```http request
GET  /sports/stream/{version}/GetOutrights?language=cs
Accept: text/event-stream
Accept-Encoding: br, gzip, deflate(如果可以使用Header)
```

| Parameter | Description |
| ------ | ------ |
| query | 使用Odata指定特定格式的查询 |
| from | 指定赛事开始日期，可以单独输入 |
| until | 指定赛事结束日期，可以单独输入 |
| language | 指定欲回应的数据语系，请参阅[Language Table](/j33app2/sports/wiki/Language-Table) |
| token | 透过 /login或/refreshToken 获得JWT token |

## Response
```
id: string\r\n
data: {
    "status": int,
    "message":string,
    "payload": {
        "outrights":{
            "add": Outright[],
            "change":OutrightChange[],
            "remove":[leagueId1,leagueId2...]
        }   
    }
}\r\n\r\n
```
| Name| Format | Description |
| ------ | ------ | ------ |
|id|string|Server Sent Event的序列号码| 
|data|json||

### Data object
| Name| Format | Description |
| ------ | ------ | ------ |
|status|int|回应的状态代码|
|message|string|回应的状态信息|
|payload|object| |

#### Payload object
| Name| Format | Description |
| ------ | ------ | ------ |
|outrights|object|优胜冠军信息列表|

##### Outrights object
| Name| Format | Description |
| ------ | ------ | ------ |
|add|Outright array|新添加的优胜冠军信息<br>- Outright 请参阅[GetOutrights](/j33app2/sports/wiki/GetOutrights) |
|change|OutrightChange array|更新的优胜冠军信息<br>- OutrightChange 请参阅[OutrightChange](/j33app2/sports/wiki/SSE-OutrightChange-Information).|
|remove|int array|删除的优胜冠军联赛ID列表|

## Status Enumeration
| status状态代码 | message显示讯息 | Description说明描述 | 
| ------ | ------ | ------ |
|0|Success|成功|
|1|InitialData|初始数据|
|3|Reset|重新连接|
|97|Invalid Accept-Encoding|Http Status Code = 400<br>无效的編碼压缩格式|
|98|Invalid OData query attributes|Http Status Code = 400<br>Odata查询属性无效或不支援|
|99|System under maintenance|Http Status Code = 503<br>系统正在维护中|
|100|Internal Server Error|Http Status Code = 500<br>服务器发生非预期错误|

* 第一次连线成功会回传status ```1```, ```add```为初始数据,使用者应当使用该讯息之```add```数据进行前端画面渲染; 接着陆续收到status```0```的更新數據```add```/```change```/```remove```
  <br><br>
* 若中途使用者因网路问题或者其他因素断线：
    * 如果是使用 browser 的 native javascript EventSource api，不关闭页面的情境下 browser 会自动重连并且自动在 header 带入 Last-Event-Id， Server 端会根据该 Last-Event-Id 透过内部资料缓存机制尝试发送该重连之 client 遗漏的更新数据
    * 如果是其他语言开发的使用者, 需自行实作重新连线机制且于header带入Last-Event-Id
    * 若缓存中找不到可发送的更新数据,则会重新产生连线status```3```,且资料内容为初始数据,使用者应当使用该讯息之```add```数据重新进行前端画面渲染
