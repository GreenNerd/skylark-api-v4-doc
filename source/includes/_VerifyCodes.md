# VerifyCodes

scope 为 `verify_code`。成功都是空正文的 201。

## 发送验证码

```http
POST /api/v4/verify_code HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "phone": "13800138000"
}
```

```http
HTTP/1.1 201 Created
```

`POST /api/v4/verify_code`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| phone | string | 是 | 接收短信的手机号 |

失败时 `errors` 是验证码服务返回的数组。

## 校验验证码

```http
POST /api/v4/verify_code/verify HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "phone": "13800138000",
  "code": "123456"
}
```

```http
HTTP/1.1 201 Created
```

失败：

```http
HTTP/1.1 422 Unprocessable Entity

{
  "errors": ["验证码校验失败"]
}
```

`POST /api/v4/verify_code/verify`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| phone | string | 是 | 手机号 |
| code | string | 是 | 验证码 |
