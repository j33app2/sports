Query是用于请求特定数据URL的一部份，如下所述，我们使用Odata Query格式，可以更弹性及便利的查询。通常您会使用：**$filter**, **$orderby**, **$top**, **$skip**。

#### **Odds Direct API 支持 Odata Query的项目**
| 参数 | 说明描述 | 例子 |
| ------ | ------ | ------ |
|$filter | 透过URL筛选数据 | $filter=sporttype eq 1|
|$orderby| 将数据排序<br>- ASC： 从小到大 <br>- DESC： 从大到小 | $orderby=sporttype desc|
|$top | 指定仅回传前几笔信息 | $top=50<br>**$top 最多支援50笔**|
|$skip | 指定略过前几笔信息| $Skip=50|
|& | 允许组合使用多个Odata Query项目 | $filter=sporttype eq 1&$top=50|

#### **support odata options**
| 运算符 | 说明描述 | 例子 |
| ------ | ------ | ------ |
| eq | 等于 | $filter=sporttype eq 1|
| ne | 不等于 | $filter=sporttype ne 2|
| lt | 小于 | $filter=bettype lt 20|
| le | 小于等于 | $filter=bettype le 20|
| gt | 大于 | $filter=bettype gt 20|
| ge | 大于等于 | $filter=bettype ge 20|
| in | 在某列表中 | $filter=sporttype in (1,2)|
| or | 或 | $filter=sporttype eq 1 or sporttype eq 2|
| and | 和 | $filter=sporttype eq 1 and isparlay eq true|
| contains | 包含某些信息 | $filter=contains(leagueName,'NBA')|
