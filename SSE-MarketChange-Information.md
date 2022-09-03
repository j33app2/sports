```
[
    {
        marketId,
        isLive,
        marketStatus,
        selections:[
            { 
                key,
                point,
                point2,
                oddsPrice:{
                    parlayPrice,
                    malayPrice,
                    decimalPrice,
                    hongKongPrice,
                    indoPrice,
                    americanPrice
                }
            }
        ]
    }
]
```

| Name| Format | Description |
| ------ | ------ | ------ |
|marketId|int|盘口ID|
|isLive|bool|是否为滚球赛事|
|marketStatus|string|盘口状态<br>running / suspend / closePrice / closed|
|sort|int|排序球头<br>当投注类型bet type=1,3,7,8且有多球头时|
|selections|SelectionInfo[]|盘口赔率项目列表|

#### SelectionInfo
| Name| Format | Description |
| ------ | ------ | ------ |
|key|string|投注类型选项|
|point|decimal?|球头|
|point2|decimal?|球头2<br>Only for bet type=646;<br> point=HDP, point2=OU|
|oddsPrice|OddsPriceInfo|赔率相关信息|

##### OddsPriceInfo
| Name| Format | Description |
| ------ | ------ | ------ |
|parlayPrice|decimal|串关赔率|
|malayPrice|decimal|马来盘赔率|
|hongKongPrice|decimal|香港盘赔率|
|decimalPrice|decimal|欧洲盘赔率|
|indoPrice|decimal|印度尼西亚盘赔率|
|americanPrice|decimal|美国盘赔率|
