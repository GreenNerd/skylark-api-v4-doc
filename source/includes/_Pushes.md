# Pushes

scope 为 `push`。成功是空正文的 200。任务异步发送。

`openids` 不能为空。`news_entity` 与 `template_entity` 至少要有一个。若带了 `template_entity`，必须同时有 `template_id` 和 `data`。

当前实现在校验模板是否被拉黑时，总会读取 `template_entity.template_id`。只传 `news_entity` 会出错并返回 500。调用时请同时提供合法的 `template_entity`。模板 id 已被标记为非法时，422 的 `errors` 是字符串：`模版ID不合法，请登录腾讯后台验证模版ID`。

## 微信推送

```http
POST /api/v4/pushes/wechat HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "openids": ["oEXAMPLE"],
  "news_entity": {
    "articles": [
      {
        "title": "标题",
        "description": "摘要",
        "url": "https://example.com/post/1",
        "picurl": "https://example.com/cover.png"
      }
    ]
  },
  "template_entity": {
    "template_id": "TEMPLATE_ID_EXAMPLE",
    "url": "https://example.com/post/1",
    "data": {
      "first": { "value": "你好", "color": "#173177" },
      "keyword1": { "value": "示例", "color": "#173177" }
    }
  }
}
```

```http
HTTP/1.1 200 OK
```

`POST /api/v4/pushes/wechat`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| openids | string[] | 是 | 接收人 openid |
| news_entity | object | 否 | 图文。单独发送时当前实现会出错 |
| template_entity | object | 否 | 模板消息。若出现，必须含 `template_id` 与 `data` |
| template_entity.template_id | string | 条件 | 模板 id |
| template_entity.data | object | 条件 | 模板字段 |
| template_entity.url | string | 否 | 点击跳转 |
