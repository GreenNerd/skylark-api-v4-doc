# Wechat Client

scope 为 `wechat_client`。`access_token` 和 `jsapi_ticket` 在 `expired_at` 之前可以缓存。不要拿 `access_token` 再去微信换 `jsapi_ticket`，票据以这里返回的为准。

示例里的令牌是占位符。

## access_token

```http
GET /api/v4/wechat_clients/access_token HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "access_token": "<wechat-access-token>",
  "expired_at": "2026-01-01T02:00:00.000+08:00"
}
```

`GET /api/v4/wechat_clients/access_token`

## jsapi_ticket

```http
GET /api/v4/wechat_clients/jsapi_ticket HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "ticket": "<wechat-jsapi-ticket>",
  "expired_at": "2026-01-01T02:00:00.000+08:00"
}
```

`GET /api/v4/wechat_clients/jsapi_ticket`
