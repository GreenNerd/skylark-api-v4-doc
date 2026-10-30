# Users

本节接口的 scope 是 `default`，除非单独写出。用户对象的字段见 [Column Explanation](#column-explanation)。

## 查询当前空间下所有用户

分页。标签只有 `id` 和 `name`。

```http
GET /api/v4/users?page=1&per_page=24 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK
X-SLP-Current-Page: 1
X-SLP-Total-Pages: 1
X-SLP-Total-Count: 1

[
  {
    "id": 1,
    "name": "示例用户",
    "nickname": "示例",
    "sex": null,
    "phone": "13800138000",
    "identifier": "13800138000",
    "openid": "oEXAMPLE",
    "binded_at": null,
    "headimgurl": "https://example.com/avatar.png",
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "tags": [{ "id": 1, "name": "成员" }],
    "organizations": [
      { "id": 1, "name": "示例组织", "description": null, "created_at": "2026-01-01T00:00:00.000+08:00" }
    ],
    "profile_submission": {
      "entries": [
        {
          "id": 1,
          "field_id": 1,
          "option_id": null,
          "value": "示例",
          "choice_id": null,
          "value_id": null,
          "latitude": null,
          "longitude": null,
          "group_id": null,
          "detail_id": null
        }
      ]
    }
  }
]
```

`GET /api/v4/users`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 所在组织

这是 GET，没有请求体。返回的组织字段比组织列表少，见 Column Explanation。

```http
GET /api/v4/users/1/organizations HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "name": "示例组织",
    "description": null,
    "description_text": null,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "children_count": 0,
    "parent_id": null,
    "ancestry": null
  }
]
```

`GET /api/v4/users/:id/organizations`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 用户 id |

## 查询用户信息

没有实名时，实名接口返回 JSON `null`。本接口在有资料时包含 `profile_submission`。

```http
GET /api/v4/users/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "name": "示例用户",
  "nickname": "示例",
  "sex": null,
  "phone": "13800138000",
  "identifier": "13800138000",
  "openid": "oEXAMPLE",
  "binded_at": null,
  "headimgurl": "https://example.com/avatar.png",
  "created_at": "2026-01-01T00:00:00.000+08:00",
  "updated_at": "2026-01-01T00:00:00.000+08:00",
  "tags": [{ "id": 1, "name": "成员" }],
  "organizations": [
    { "id": 1, "name": "示例组织", "description": null, "created_at": "2026-01-01T00:00:00.000+08:00" }
  ]
}
```

`GET /api/v4/users/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 用户 id |

## 创建用户

成功是 200，正文与用户详情相同。校验失败是模型 `errors` 对象。

`entries_attributes` 的字段见 Column Explanation。

```http
POST /api/v4/users HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "name": "示例用户",
  "identifier": "13800138000",
  "phone": "13800138000",
  "openid": "oEXAMPLE",
  "headimgurl": "https://example.com/avatar.png",
  "tag_ids": [1],
  "profile_submission_attributes": {
    "entries_attributes": [
      {
        "value": "示例",
        "field_id": 1,
        "option_id": null,
        "choice_id": null,
        "value_id": null,
        "longitude": null,
        "latitude": null,
        "group_id": null
      }
    ]
  }
}
```

`POST /api/v4/users`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| name | string | 否 | 姓名 |
| identifier | string | 否 | 识别码 |
| phone | string | 否 | 手机号 |
| openid | string | 否 | 微信 openid |
| headimgurl | string | 否 | 头像地址 |
| tag_ids | integer[] | 否 | 用户标签 id |
| profile_submission_attributes | object | 否 | 含 `entries_attributes` |

## 更新用户

路径必须带用户 id。`PUT` 与 `PATCH` 都可以。成功返回用户详情。

校验失败时，当前实现把错误交给一个未赋值的组织对象。最终正文是再编码过一次的 JSON 字符串，内容为 `{"errors":["参数错误"]}`，看不到具体字段错误。

```http
PUT /api/v4/users/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "name": "示例用户",
  "identifier": "13800138000",
  "phone": "13800138000",
  "openid": "oEXAMPLE",
  "headimgurl": "https://example.com/avatar.png",
  "tag_ids": [1]
}
```

`PUT /api/v4/users/:id`

`PATCH /api/v4/users/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 用户 id |
| name | string | 否 | 姓名 |
| identifier | string | 否 | 识别码 |
| phone | string | 否 | 手机号 |
| openid | string | 否 | 微信 openid |
| headimgurl | string | 否 | 头像地址 |
| tag_ids | integer[] | 否 | 用户标签 id |
| profile_submission_attributes | object | 否 | 含 `entries_attributes` |

## 更新用户标签

成功返回用户详情。标签必须是当前空间的用户标签。

```http
POST /api/v4/users/1/tags HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "add_tag_ids": [1],
  "remove_tag_ids": [2]
}
```

`POST /api/v4/users/:id/tags`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 用户 id |
| add_tag_ids | integer[] | 否 | 要加上的标签 |
| remove_tag_ids | integer[] | 否 | 要去掉的标签 |

## 查询实名信息

没有记录时正文是 JSON `null`，不是空对象。有记录时为 `{ "id", "data" }`。

```http
GET /api/v4/users/1/identity_certification HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

null
```

`GET /api/v4/users/:id/identity_certification`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 用户 id |

## 查询用户

`query_type` 默认 `phone`，按姓名或手机号。设为 `identifier` 时按姓名或识别码。`ids` 可与关键字一起用。分页。

```http
GET /api/v4/users/query?keyword=示例&query_type=phone&ids[]=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/users/query`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| keyword | string | 否 | 姓名、手机号或识别码 |
| query_type | string | 否 | `phone`（默认）或 `identifier` |
| ids | integer[] | 否 | 只保留这些用户 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

响应与用户列表相同。

## 任务统计

只统计处理人任务。`process_count` 是处理中数量，`assignment_count` 是已处理数量，不是两者之和。

```http
GET /api/v4/users/assignment_stats?organization_id=1&user_ids[]=1&flow_ids[]=1&created_at_gt=2026-01-01&created_at_lt=2026-12-31 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "name": "示例用户",
    "process_count": 1,
    "assignment_count": 2,
    "overdue_processing_count": 0,
    "overdue_processed_count": 0
  }
]
```

`GET /api/v4/users/assignment_stats`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 否 | 该组织及其下级的成员 |
| user_ids | integer[] | 否 | 限定用户 |
| flow_ids | integer[] | 否 | 限定流程 |
| created_at_gt | time | 否 | 流程创建时间下界 |
| created_at_lt | time | 否 | 流程创建时间上界 |

## 用户的延期申请

路径上的用户会被加载，但查询用的是当前登录用户，不是路径里的 `:id`。只带 ApiApplication 的 JWT 时不会登录用户，这个列表通常是空的。分页。可选 `status`。

字段见 Column Explanation 的延期申请。

```http
GET /api/v4/users/1/delay_requests?status=processing&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/users/:id/delay_requests`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 路径上的用户 id。查询实际用的是当前登录用户 |
| status | string | 否 | 延期申请状态 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 签发登录令牌

scope 为 `user_login_token`。配置里的 `v4.login.enable` 未打开时返回 403。令牌约 60 秒过期，payload 含 `user_gid` 与 `exp`。

```http
POST /api/v4/user_login_token HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "user_id": 1
}
```

```http
HTTP/1.1 200 OK

{
  "user_login_token": "<user-jwt>"
}
```

`POST /api/v4/user_login_token`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 当前空间的用户 |

## 用户资料结构

```http
GET /api/v4/user_profile/schema HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "namespace_id": 1,
  "fields": [
    {
      "id": 1,
      "title": "姓名",
      "description": null,
      "type": "Field::Text",
      "position": 1,
      "validations": [],
      "other_option": false,
      "visibility": null,
      "marked": false,
      "settings": {},
      "detail_id": null,
      "identity_key": null,
      "data": {},
      "maximum": null
    }
  ]
}
```

`GET /api/v4/user_profile/schema`
