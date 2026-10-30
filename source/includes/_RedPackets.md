# RedPackets

scope 为 `red_packet`。接口只投递任务，成功是空正文的 200。`amount` 会转成整数。

## 发放

```http
POST /api/v4/red_packets/transmit HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "user_id": 1,
  "amount": 100,
  "options": {
    "wishing": "恭喜",
    "act_name": "活动",
    "remark": "备注"
  }
}
```

```http
HTTP/1.1 200 OK
```

`POST /api/v4/red_packets/transmit`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 当前空间的用户 |
| amount | integer | 是 | 金额 |
| options[wishing] | string | 是 | `options` 整体必填 |
| options[act_name] | string | 否 | 活动名 |
| options[remark] | string | 否 | 备注 |
