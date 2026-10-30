# Forms

scope 为 `default`。表单、字段、记录和条目的字段见 [Column Explanation](#column-explanation)。

## 表单信息

```http
GET /api/v4/forms/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "title": "示例表单",
  "description": null,
  "created_at": "2026-01-01T00:00:00.000+08:00",
  "updated_at": "2026-01-01T00:00:00.000+08:00",
  "status": "published",
  "identity_vertify_type": null,
  "logic_settings": {},
  "external_settings": {},
  "closed_at": null,
  "responses_limit": null,
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
      "maximum": null,
      "options": [
        { "id": 1, "value": "选项", "settings": {}, "position": 1 }
      ]
    }
  ],
  "user_boundary": {
    "id": 1,
    "organization_ids": [],
    "user_tag_ids": [],
    "user_tagged_type": null,
    "only_binded": false,
    "user_ids": []
  },
  "webhooks": [
    {
      "id": 1,
      "type": "Webhook",
      "subscribed_events": ["ResponseCreateEvent"],
      "payload_url": "https://example.com/hooks"
    }
  ]
}
```

`GET /api/v4/forms/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 表单 id |

明细字段会多 `children`，级联字段会多 `cascaded_select`。

## 创建表单

`user_id` 必填，作为创建者。成功 201，正文与表单详情相同。失败是模型 `errors` 对象。

`fields_attributes`、`user_boundary_attributes` 的可传键见 Column Explanation。

```http
POST /api/v4/forms?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "form": {
    "title": "示例表单",
    "description": "说明",
    "anonymous_allowed": false,
    "enable_appendable": false,
    "submit_once": false,
    "involved_queryable": false,
    "step_renderable": false,
    "status": "published",
    "response_required": false,
    "cloned_from_id": null,
    "after_submit_action": null,
    "after_submit_show_message": null,
    "after_submit_redirect_url": null,
    "success_message": null,
    "published_as_id": null,
    "namecard_id": null,
    "attachment_ids": [],
    "tag_ids": [],
    "slp_index": null,
    "responses_limit": null,
    "closed_at": null,
    "comment_status": null,
    "settings": {
      "responses_sharing": null,
      "marked_field_ids": [],
      "table_mapping": null
    },
    "red_packet_setting_attributes": {
      "wishing": "恭喜",
      "act_name": "活动",
      "remark": "备注",
      "send_name": "示例",
      "per_amount": 1,
      "begin_per_amount": 1,
      "end_per_amount": 1,
      "expired_at": null,
      "random": false,
      "total_num": 1
    },
    "fields_attributes": [
      {
        "title": "姓名",
        "type": "Field::Text",
        "position": 1
      }
    ],
    "user_boundary_attributes": {
      "only_binded": false,
      "user_tagged_type": null,
      "user_tag_ids": [],
      "user_ids": [],
      "organization_ids": []
    },
    "push_agent_on_publish_attributes": {
      "include_uncompleted": false,
      "push_package_id": null,
      "scheduled_at": null
    },
    "webhooks_attributes": [
      {
        "type": "Webhook",
        "payload_url": "https://example.com/hooks",
        "subscribed_events": ["ResponseCreateEvent"]
      }
    ]
  }
}
```

`POST /api/v4/forms`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 创建者 |
| form | object | 是 | 上例中的全部键。字段嵌套见 Column Explanation |

## 更新表单

`PUT` 与 `PATCH` 都可以。`user_id` 必填。比创建多 `identity_vertify_type`、`identity_vertify_notice`、`external_settings`。`settings` 还可含 `location_exporting`、`primary_field_id`。webhook 还可含 `id`、`_destroy`。字段更新可带 `id` 与 `_destroy`。

```http
PATCH /api/v4/forms/1?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "form": {
    "title": "示例表单",
    "identity_vertify_type": null,
    "identity_vertify_notice": null,
    "external_settings": {}
  }
}
```

`PUT /api/v4/forms/:id`

`PATCH /api/v4/forms/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 表单 id |
| user_id | integer | 是 | 修改人 |
| form | object | 是 | 与创建相同。另含 `identity_vertify_type`、`identity_vertify_notice`、`external_settings`。`settings` 还可含 `location_exporting`、`primary_field_id`。webhook 还可含 `id`、`_destroy`。字段更新可带 `id` 与 `_destroy` |

# Responses

记录嵌套在表单下。单条读取和删除在 `/api/v4/responses/:id`。

## 表单数据

默认 `id desc`。`order=asc` 改为升序。分页。每条含 `entries` 和 `user`。

```http
GET /api/v4/forms/1/responses?order=asc&page=1&per_page=24 HTTP/1.1
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
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "cached_values": {},
    "mapped_values": {},
    "involved_user_ids": [],
    "involved_organization_ids": [],
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
    ],
    "user": {
      "id": 1,
      "name": "示例用户",
      "phone": "13800138000",
      "identifier": "13800138000"
    }
  }
]
```

`GET /api/v4/forms/:form_id/responses`

示例里的 `user` 只保留了识别字段。实际对象是 Column Explanation 里的完整 v4 用户。

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 id |
| order | string | 否 | `asc` 为升序，否则按 id 降序 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 查询单条数据

记录必须属于当前空间。

```http
GET /api/v4/responses/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/responses/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 记录 id |

正文与列表中的单条相同，用户对象是完整 v4 用户。

## 提交记录

`user_id` 必填。表单已关闭时 422，`errors` 为字符串 `"表单已经关闭"`。

```http
POST /api/v4/forms/1/responses?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "response": {
    "entries_attributes": [
      {
        "field_id": 1,
        "value": "示例",
        "option_id": null,
        "choice_id": null,
        "value_id": null,
        "longitude": null,
        "latitude": null,
        "group_id": null,
        "slp_index": null
      }
    ]
  }
}
```

`POST /api/v4/forms/:form_id/responses`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 id |
| user_id | integer | 是 | 填写人 |
| response[entries_attributes] | object[] | 否 | 见 Column Explanation，另含 `slp_index` |

## 更新记录

路径在表单下面，必须带 `form_id`。`PUT` 与 `PATCH` 都可以。条目带 `id` 时更新已有条目，`_destroy` 为真时删除。

```http
PATCH /api/v4/forms/1/responses/1?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "response": {
    "entries_attributes": [
      {
        "id": 1,
        "field_id": 1,
        "value": "示例",
        "_destroy": false,
        "slp_index": null
      }
    ]
  }
}
```

`PUT /api/v4/forms/:form_id/responses/:id`

`PATCH /api/v4/forms/:form_id/responses/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 id |
| id | integer | 是 | 记录 id |
| user_id | integer | 是 | 填写人 |
| response[entries_attributes] | object[] | 否 | 见 Column Explanation。带 `id` 时更新，`_destroy` 为真时删除，另含 `slp_index` |

## 搜索表单记录

`query` 的键是字段 id 或虚拟字段 id，见 Column Explanation。`order` 只使用第一对。分页。

```http
GET /api/v4/forms/1/responses/search?query[12]=示例&query[-1]=2026-01-01&query[-2]=1&query[-3]=1&query[-18]=13800138000&query[-20]=13800138000&order[-1]=desc&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/forms/:form_id/responses/search`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 id |
| query | object | 否 | 字段 id 或 -1、-2、-3、-18、-20 |
| order | object | 否 | 一个字段 id 到 `asc` 或 `desc` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 导出

创建导出任务后返回空的 200。文件从 [Exportable files](#exportable-files) 下载。`user_id` 必填。

`enhanced` 为真时还可传 `query`。否则可传 `organizations` 和 `filled_at`。

```http
GET /api/v4/forms/1/responses/export?user_id=1&enhanced=1&field_ids[]=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK
```

`GET /api/v4/forms/:form_id/responses/export`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 id |
| user_id | integer | 是 | 导出文件的所属用户 |
| enhanced | boolean | 否 | 为真时走增强导出，并可带 `query` |
| field_ids | integer[] | 否 | 导出的字段 |
| organizations | string | 否 | 非增强导出的组织筛选 |
| filled_at | string | 否 | 非增强导出的填写时间 |
| query | object | 否 | 仅增强导出 |

## 下载导入模板

响应是 xlsx 文件，不是 JSON。

```http
GET /api/v4/forms/1/responses/download_template HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK
Content-Disposition: attachment; filename="示例表单-导入模板.xlsx"
Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet

<xlsx bytes>
```

`GET /api/v4/forms/:form_id/responses/download_template`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 id |

## 批量删除

立刻返回 204，实际删除异步执行。`_destroy_all` 为真时删除该表单全部记录，否则按 `ids`。表单已关闭时 422。

```http
DELETE /api/v4/forms/1/responses/batch_destroy?ids[]=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/forms/:form_id/responses/batch_destroy`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 id |
| ids | integer[] | 否 | 要删除的记录。与 `_destroy_all` 二选一 |
| _destroy_all | boolean | 否 | 为真时删除全部 |

## 删除单条记录

```http
DELETE /api/v4/responses/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/responses/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 记录 id |
