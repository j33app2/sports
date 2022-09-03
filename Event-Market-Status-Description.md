| Event Status | Market Status | Selection | Frontend Display | PlaceBet |
| ------ | ------ | ------| ------ | ------ |
| running | running | Yes | **是 Yes** | **是 Yes** |
| running | suspend | Yes | **是 Yes** | 否 No |
| running | closeprice | Yes | 否 No | 否 No |
| running | closed | Empty| 否 No | 否 No |

| Event Status | Market Status | Selection | Frontend Display | PlaceBet |
| ------ | ------ | ------| ------ | ------ |
| postponed | running | Yes | 否 No | 否 No |
| postponed | suspend | Yes | 否 No | 否 No |
| postponed | closeprice | Yes | 否 No | 否 No |
| postponed | closed | Empty| 否 No | 否 No |

| Event Status | Market Status | Selection | Frontend Display | PlaceBet |
| ------ | ------ | ------| ------ | ------ |
| closed | closed | Empty | 否 No | 否 No |



## Market Status Note: 
* running: 盘口开启可下注
* suspend: 盘口暂时关闭 (游戏前端可见赔率但无法下注)
* closeprice: 盘口暂时关闭 (赔率隐藏且该下注区域可闪烁提示玩家。賠率關閉原因可能因进球, 红牌或是其他任何事件让球赛中断)
* closed: 盘口关闭