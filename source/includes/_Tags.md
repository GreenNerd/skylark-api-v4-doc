# Tags

`GET /tags` 的 `type` 只能是 `user` 或 `receipt`，放在查询字符串里。其他值返回空数组。标签字段是 `id`、`name`、`full_name`。

分页函数的返回值没有赋回，响应头和正文可能不一致，见 [Pagination](#pagination)。

## 查询空间下标签类型

```http
GET /api/v4/tags?type=user HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  { "id": 1, "name": "成员", "full_name": "成员" }
]
```

`GET /api/v4/tags`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| type | string | 是 | `user` 或 `receipt` |

## 按名称查询标签

`keyword` 是 PostgreSQL 正则，不是普通子串。`type` 同样只接受 `user` 或 `receipt`。

```http
GET /api/v4/tags/query?type=user&keyword=成员 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/tags/query`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| type | string | 是 | `user` 或 `receipt` |
| keyword | string | 否 | 名称正则 |

## 查询成员标签下的成员

可选 `keyword`，按姓名或手机号过滤。分页。返回完整 v4 用户。

```http
GET /api/v4/tags/1/taggable_users?keyword=示例&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/tags/:id/taggable_users`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 标签 id |
| keyword | string | 否 | 姓名或手机号 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 查询标签下的表单

分页。表单字段见 [Forms](#forms) 的详情。

```http
GET /api/v4/tags/1/taggable_forms?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/tags/:id/taggable_forms`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 标签 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

# Tag groups

`type` 必填，只能是 `user`、`receipt`、`yaw`。其他值是 404。

## 标签组列表

```http
GET /api/v4/tag_groups?type=user&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  { "id": 1, "name": "默认", "type": "user", "namespace_id": 1 }
]
```

`GET /api/v4/tag_groups`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| type | string | 是 | `user`、`receipt` 或 `yaw` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 组内标签

分页，标签字段同上。

```http
GET /api/v4/tag_groups/1/tags?type=user&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/tag_groups/:id/tags`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 标签组 id |
| type | string | 是 | `user`、`receipt` 或 `yaw` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

列表和组内标签都要带 `type`，因为控制器在每个动作之前都检查它。

## 创建标签

```http
POST /api/v4/tag_groups/1/tags?type=user HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "tag": {
    "name": "成员",
    "color": "#336699"
  }
}
```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "name": "成员",
  "full_name": "成员"
}
```

`POST /api/v4/tag_groups/:tag_group_id/tags`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| tag_group_id | integer | 是 | 标签组 id |
| type | string | 是 | 查询参数，`user`、`receipt` 或 `yaw` |
| tag[name] | string | 是 | 名称 |
| tag[color] | string | 否 | 颜色 |

## 更新标签

```http
PUT /api/v4/tag_groups/1/tags/1?type=user HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "tag": {
    "name": "成员",
    "color": "#336699"
  }
}
```

`PUT /api/v4/tag_groups/:tag_group_id/tags/:id`

`PATCH /api/v4/tag_groups/:tag_group_id/tags/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| tag_group_id | integer | 是 | 标签组 id |
| id | integer | 是 | 标签 id |
| type | string | 是 | 查询参数，`user`、`receipt` 或 `yaw` |
| tag[name] | string | 是 | 名称 |
| tag[color] | string | 否 | 颜色 |

## 删除标签

```http
DELETE /api/v4/tag_groups/1/tags/1?type=user HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/tag_groups/:tag_group_id/tags/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| tag_group_id | integer | 是 | 标签组 id |
| id | integer | 是 | 标签 id |
| type | string | 是 | 查询参数，`user`、`receipt` 或 `yaw` |
