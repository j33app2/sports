此API用于取得体育视频连结

## Request
```http request
GET  /sports/{version}/GetStreaming?sportType=xx&streamingOption=xx&channelCode=xx
Accept: application/json
Accept-Encoding: br, gzip, deflate
X-Forwarded-For: client ip (如果通过代理使用API需要额外带入)
Authorization: Bearer {JWT token}
```
| Parameter | Format | Mandatory | Description |
| ------ | ------ | ------ | ------ |
|sportType|int|Yes|体育项目ID|
|streamingOption|int|Yes|视频ID (从`/GetEvents`API 取得)|
|channelCode|string|Yes|视频代码 (从`/GetEvents`API 取得)<br>* 需要先**url encode** 再带入|

## Response
```
{    
    "StreamingUrl": string?,
    "StreamingUrlH5": string?,
    "StreamingUrlCN": string?,
    "StreamingUrlNonCN": string?, 
    "StreamingUrlStreamer": string?
} 
```
| Name| Format | Description | Queryable | Query Example |
| ------ | ------ | ------ | ------ | ------ |
|streamingUrl|string?|H5 的.m3u8格式视频链结<br>需要使用 videojs 来播放影片, 作法可以参考[这里](https://videojs.github.io/videojs-contrib-hls/)|No|—|
|streamingUrlH5|string?|H5 视频链结|No|—|
|streamingUrlCN|string?|.m3u8 格式视频链结(用于中国观看者)|No|—|
|streamingUrlNonCN|string?|.m3u8 格式视频链结(用于非中国观看者)|No|—|
|streamingUrlStreamer|string?|主播串流视频链结|No|—|

