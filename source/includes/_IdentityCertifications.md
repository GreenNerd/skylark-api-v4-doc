# IdentityCertifications

scope 为 `identity_certifications`。人脸链接和绑定是两个不同的路径。响应里的核身地址键名是代码中的拼写 `identity_vertify_url`。

## 获取人脸核身的链接

```http
GET /api/v4/identity_certifications/new?redirect_url=https://example.com/done&user_name=示例&id_card=ID_CARD_EXAMPLE HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "identity_vertify_url": "https://example.com/detect"
}
```

`GET /api/v4/identity_certifications/new`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| redirect_url | string | 是 | 核身完成回跳地址 |
| user_name | string | 是 | 姓名 |
| id_card | string | 是 | 证件号 |

## 用户绑定授权信息

成功 201。`BizToken` 的大小写要与参数名一致。

```http
GET /api/v4/identity_certifications/auth?user_id=1&BizToken=BIZ_TOKEN_EXAMPLE HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 201 Created

{
  "message": "实名信息创建成功"
}
```

`GET /api/v4/identity_certifications/auth`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 当前空间的用户 |
| BizToken | string | 是 | 核身返回的 token |

## 查询核身结果

参数名是小写的 `biz_token`。正文是腾讯核身结果本身，没有固定的本地字段表。

```http
GET /api/v4/identity_certifications/get_detect_info?biz_token=BIZ_TOKEN_EXAMPLE HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/identity_certifications/get_detect_info`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| biz_token | string | 是 | 核身 token |
