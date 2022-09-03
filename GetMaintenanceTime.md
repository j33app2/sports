此API用于获取系统维护时间

## **Request**
```http request
GET /login/GetMaintenanceTime
Content-Type: application/json
```

## **Response**
```
{
    "isUnderMaintenance": bool,
    "startTime": datetime?,
    "endTime": datetime?
}
```
| Parameter | Format | Description |
| ------ | ------ | ------ |
|isUnderMaintenance|bool|是否维护期间|
|startTime|datetime?|维护起始时间 (时区 GMT+0).|
|endTime|datetime?|维护结束时间 (时区 GMT+0).|