# Organizations

读取、更新、删除组织，以及 `GET /organizations/:id/members`，scope 是 `organization_user`。

`POST /organizations`、嵌套的成员接口、管理员接口，scope 是 `manage_organization`。

组织对象见 [Column Explanation](#column-explanation)。更新同时接受 `PUT` 和 `PATCH`。

## 所有组织

分页。包含 `ancestor_names` 和资料条目。

```http
GET /api/v4/organizations?page=1&per_page=24 HTTP/1.1
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
    "name": "示例组织",
    "description": null,
    "description_text": null,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "children_count": 0,
    "parent_id": null,
    "ancestry": null,
    "ancestor_names": [],
    "application_strategy": "must_approved"
  }
]
```

`GET /api/v4/organizations`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 组织详情

在组织字段之外还有四个统计字段。

```http
GET /api/v4/organizations/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "name": "示例组织",
  "description": null,
  "description_text": null,
  "created_at": "2026-01-01T00:00:00.000+08:00",
  "updated_at": "2026-01-01T00:00:00.000+08:00",
  "children_count": 0,
  "parent_id": null,
  "ancestry": null,
  "ancestor_names": [],
  "application_strategy": "must_approved",
  "apply_link": "https://beta.skylarkly.com/namespaces/1/organizations/1",
  "members_count": 1,
  "binded_members_count": 0,
  "pending_organization_applications_count": 0
}
```

`GET /api/v4/organizations/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |

## 顶级组织

响应与组织列表相同。

```http
GET /api/v4/organizations/roots HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/organizations/roots`

## 按名称查询

`name` 默认按 PostgreSQL 正则匹配（`name ~ :name`）。代码用 `params.fetch(:regexp_match, true)` 判断。查询字符串里的 `regexp_match=false` 是字符串，在 Ruby 里仍为真，正则不会关闭。

分页之后又调用了 `reorder`，但没有写回变量，所以响应顺序不一定按名称。

```http
GET /api/v4/organizations/query?name=示例&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/organizations/query`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| name | string | 是 | 组织名称或正则 |
| regexp_match | boolean | 否 | 默认开启正则。GET 查询字符串无法把它关掉 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 子代组织

直接子组织，响应与组织列表相同。路径参数是 `:id`。

```http
GET /api/v4/organizations/1/children HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/organizations/:id/children`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |

## 全部后代

分页，含下级的下级。

```http
GET /api/v4/organizations/1/descendants?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/organizations/:id/descendants`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 创始人

返回完整 v4 用户对象。

```http
GET /api/v4/organizations/1/founder HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/organizations/:id/founder`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |

## 组织成员

路径参数是 `:id`，不是 `:organization_id`。分页。成员没有 `headimgurl`，有 `tag_ids` 和 `tags`（`id`、`name`、`full_name`）。`with_descendants` 有值时包含下级组织的成员。

```http
GET /api/v4/organizations/1/members?with_descendants=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "name": "示例用户",
    "nickname": "示例",
    "sex": null,
    "phone": "13800138000",
    "identifier": "13800138000",
    "openid": "oEXAMPLE",
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "tag_ids": [1],
    "tags": [{ "id": 1, "name": "成员", "full_name": "成员" }]
  }
]
```

`GET /api/v4/organizations/:id/members`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |
| with_descendants | string | 否 | 有值时包含下级成员 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 按标签筛选成员

`tag_id` 必填。范围是该组织子树。分页。返回完整 v4 用户。

```http
GET /api/v4/organizations/1/taggable_members?tag_id=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/organizations/:id/taggable_members`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |
| tag_id | integer | 是 | 标签 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 创建组织

scope 为 `manage_organization`。`founder_id` 必须是当前空间的用户，`parent_id` 若出现必须是当前空间的组织，否则 422，`errors` 为字符串数组。成功 201，正文是组织对象。父级字段名是 `parent_id`。

```http
POST /api/v4/organizations HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "parent_id": null,
  "name": "示例组织",
  "description": "说明",
  "application_strategy": "must_approved",
  "founder_id": 1,
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
        "_destroy": false,
        "group_id": null
      }
    ]
  }
}
```

`POST /api/v4/organizations`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| parent_id | integer | 否 | 上级组织 |
| name | string | 是 | 名称 |
| description | string | 否 | 说明 |
| application_strategy | string | 否 | `must_approved`、`auto_approved`、`closed` |
| founder_id | integer | 是 | 创始人用户 id |
| profile_submission_attributes | object | 否 | 含 `entries_attributes` |

## 修改组织信息

`parent_id` 和 `founder_id` 会被丢掉，不能用这个接口改上级或创始人。成功 200，正文是组织对象。

```http
PUT /api/v4/organizations/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "name": "示例组织",
  "description": "说明",
  "application_strategy": "auto_approved"
}
```

`PUT /api/v4/organizations/:id`

`PATCH /api/v4/organizations/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |
| name | string | 否 | 名称 |
| description | string | 否 | 说明 |
| application_strategy | string | 否 | `must_approved`、`auto_approved`、`closed` |

## 删除组织

```http
DELETE /api/v4/organizations/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/organizations/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 组织 id |

# Members

以下接口的路径参数是 `:organization_id`，scope 为 `manage_organization`。

## 创建组织成员

在当前空间新建用户并加入该组织。成功 201，正文是成员用户（含 `tag_ids`）。

```http
POST /api/v4/organizations/1/members HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "name": "示例用户",
  "identifier": "13800138000",
  "phone": "13800138000",
  "tag_ids": [1]
}
```

`POST /api/v4/organizations/:organization_id/members`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| name | string | 否 | 姓名 |
| identifier | string | 否 | 识别码 |
| phone | string | 否 | 手机号 |
| tag_ids | integer[] | 否 | 用户标签 |

## 修改组织成员信息

`:id` 是成员用户 id。可写字段与创建相同。

```http
PUT /api/v4/organizations/1/members/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "name": "示例用户",
  "identifier": "13800138000",
  "phone": "13800138000",
  "tag_ids": [1]
}
```

`PUT /api/v4/organizations/:organization_id/members/:id`

`PATCH /api/v4/organizations/:organization_id/members/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| id | integer | 是 | 成员用户 id |
| name | string | 否 | 姓名 |
| identifier | string | 否 | 识别码 |
| phone | string | 否 | 手机号 |
| tag_ids | integer[] | 否 | 用户标签 |

## 搜索组织成员

按姓名或手机号。分页。响应与成员列表相同。

```http
GET /api/v4/organizations/1/members/query?keyword=示例&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/organizations/:organization_id/members/query`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| keyword | string | 否 | 姓名或手机号 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 增加组织人员

把已有用户加入组织。响应是对象，不是裸数组。

```http
PUT /api/v4/organizations/1/members/add HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "member_ids": [1]
}
```

```http
HTTP/1.1 200 OK

{
  "member_ids": [1]
}
```

`PUT /api/v4/organizations/:organization_id/members/add`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| member_ids | integer[] | 否 | 要加入的用户 id |

## 移除组织成员

```http
PUT /api/v4/organizations/1/members/remove HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "member_ids": [1]
}
```

```http
HTTP/1.1 200 OK

{
  "member_ids": [1]
}
```

`PUT /api/v4/organizations/:organization_id/members/remove`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| member_ids | integer[] | 否 | 要移除的用户 id |

# Administrators

scope 为 `manage_organization`。用户对象是后台用户模板，见 Column Explanation。没有 `custom_values`。

## 查询当前组织管理员

```http
GET /api/v4/organizations/1/administrators HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "user": {
      "id": 1,
      "name": "示例用户",
      "nickname": "示例",
      "phone": "13800138000",
      "identifier": "13800138000",
      "qq": null,
      "headimgurl": "https://example.com/avatar.png",
      "openid": "oEXAMPLE",
      "imported_alias": null,
      "from_wechat": false,
      "tags": [
        {
          "id": 1,
          "name": "成员",
          "full_name": "成员",
          "color": null,
          "tag_group_id": 1,
          "taggings_count": 1
        }
      ]
    },
    "access": {
      "id": 1,
      "name": "管理员",
      "actions": [1],
      "founded": false
    },
    "organization": {
      "id": 1,
      "name": "示例组织",
      "description": null,
      "created_at": "2026-01-01T00:00:00.000+08:00"
    }
  }
]
```

`GET /api/v4/organizations/:organization_id/administrators`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |

## 增加组织管理员

成功 201，正文与列表中的单条相同。

```http
POST /api/v4/organizations/1/administrators HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "user_id": 1,
  "access_id": 1
}
```

`POST /api/v4/organizations/:organization_id/administrators`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| user_id | integer | 是 | 用户 |
| access_id | integer | 是 | 权限 |

## 修改组织管理员权限

```http
PUT /api/v4/organizations/1/administrators/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "user_id": 1,
  "access_id": 1
}
```

`PUT /api/v4/organizations/:organization_id/administrators/:id`

`PATCH /api/v4/organizations/:organization_id/administrators/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| id | integer | 是 | 管理员记录 id |
| user_id | integer | 是 | 用户 |
| access_id | integer | 是 | 权限 |

## 删除组织管理员

```http
DELETE /api/v4/organizations/1/administrators/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/organizations/:organization_id/administrators/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| organization_id | integer | 是 | 组织 id |
| id | integer | 是 | 管理员记录 id |

## 组织资料结构

scope 为 `default`。

```http
GET /api/v4/organization_profile/schema HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "namespace_id": 1,
  "fields": []
}
```

`GET /api/v4/organization_profile/schema`
