```
[
    {
        leagueId,
        eventStatus,
        teams:[
            {
                orid,
                price,
                maxBet,
                oddsStatus,
                isUpdate
            }
        ]
    }
]   
```

| Name| Format | Description |
| ------ | ------ | ------ |
|leagueId|int|联赛ID|
|eventStatus|string|优胜冠军状态<br>running/closed|
|teams|Teams|队伍相关信息|

#### Teams
| Name| Format | Description |
| ------ | ------ | ------ |
|orid|int|优胜冠军赔率ID|
|price|decimal|赔率 (欧洲盘)|
|maxBet|int|最大投注额|
|oddsStatus|string|盘口状态<br>running/closed|
|isUpdate|bool|赔率使否异动|