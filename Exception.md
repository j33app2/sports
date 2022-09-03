### 例外回传的格式
```
{
  "statusCode": int,  
  "errorCode": string,  
  "message": string, 
}
```
### Http状态代码说明
| HTTP Code | 说明描述 |
| ------ | ------ |
| 200 | 请求成功，依据请求条件回传该信息 |
| 400 | 服务器无法处理该请求，原因可能为语法错误、请求无效等 |
| 401 | 身分验证失败 |
| 403 | 该请求是有效的，但服务器拒绝存取。原因可能为用户没有其权限或可能需要某些特殊账号等 |
| 500 | 非预期的错误发生 |
| 503 | 服务器处于无法接受请求的状态|


### 错误代码说明
| Error Code| 显示讯息 | 说明描述 | 
| ------ | ------ | ------ |
| A001 | Unauthorized | login 或 refreshToken验证失败 |
| A002 | Member not found | 系统验证找不到客户信息 |
| A003 | Prohibited Visit | 客户没有访问权限 |
| E001 | Internal Server Error | 服务器发生非预期错误 |
| E002 | Invalid parameter input | 参数输入无效或不支援 |
| E003 | Invalid OData query attributes | Odata查询属性无效或不支援|
| E004 | ClientIP Is Invalid | 客户ip无效或不支援 |
| E005 | Invalid Accept-Encoding| 无效的編碼压缩格式 |
| E006 | Unauthorized vendor| 未被授权的厂商 |
| E007 | Streaming Temporarily Closed| 厂商暂时关闭体育视频 |
| B001 | Failed Execution | 系统执行失败|
| B002 | Customer Not Deposited | 客戶未存款 |
| B003 | Duplicated Transaction Id | 厂商交易编号重复 |
| B004 | Invalidate Vendor Id | 无效的厂商编号 |
| B005 | Event closed or Invalid market ID | 赛事已关闭或无效的market ID |
| B006 | E-Sport Status Changed | [**E-Sport 专用**] 赛事状态改变 ( **In-Play** 和 **Starting Soon**)|
| B007 | Score Changed | 分数已更新 |
| B008 | Point Changed | 球头已更新 |
| B009 | Point Expired | 球头已过期 |
| B010 | Odds Changed | 赔率已更新 |
| B011 | Odds Suspend | 赔率正在调整 |
| B012 | Odds Error | 赔率错误 |
| B013 | Stake Problem | 投注数量超过最大值或低于最小值 |
| B014 | Over Max Bet | 单场赛事的投注数量超过了最大值 |
| B015 | Price Closed | 价格关闭且market暂时关闭 |
| B016 | Market Closed | market已关闭 |
| B017 | Insufficient balance | 客户余额不足 |
| B018 | Disabled Bet | 账号无法投注 |
| B020 | SportType is Invalid | 无效的运动类型 |
| B021 | Under Parlay Count | 低于最低串关赛事数量 |
| B022 | Lucky Parlay Error | 串关错误 |
| B023 | Cashout Price Not Found | 未找到实时兑现的价格 |
| B024 | Event Closed | 赛事已关闭 |
| B025 | Cannot Cashout | 票不能进行实时兑现 |
| B026 | Selling Ticket Not Found | 未找到实时兑现的票 |
| B027 | Cashout Account Not Found | 客户不能进行实时兑现 |
| B028 | Customer Closed | 会员账号已关闭 |
| B029 | Parlay MaxBet Less Than MinBet | 串关最大投注额小于最小投注额 |
| B030 | Parlay No Combo Available | 超过最大 payout 请减少串关数量 |
| B031 | Parlay Exceeds MaxMarkets | 超过最多可串关数量(最多仅支持串 20 场) |
| B032 | Single Wallet Failed| 单一钱包系统执行失败 |
| B033 | Parlay Same Event| 串关使用相同的赛事 |
| B034 | Single Wallet Cannot Accept Worse Odds| 单一钱包不支援接受更差的赔率 |
| B035 | Disabled Parlay Event| 赛事禁止串关 |
| B036 | No Valid Parlay Combination| 无可使用的串关组合 |
| B037 | Duplicated Bet| 重複下注 |
| UM99 | System is under maintenance | 系统正在维护中 |
