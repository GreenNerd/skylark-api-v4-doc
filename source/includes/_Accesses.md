# Accesses

scope 为 `manage_organization`。

## 获取当前空间下所有权限

```http
GET /api/v4/accesses HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "name": "管理员",
    "actions": [1, 3],
    "founded": false
  }
]
```

`GET /api/v4/accesses`
