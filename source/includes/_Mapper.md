# Mapper

这些接口返回映射用的精简 JSON。记录没有完整 `entries`。用户是 Mapper 用户，见 [Column Explanation](#column-explanation)。

`GET /api/v4/mapper/responses` 按 `form_id` 查找表单，没有按当前空间过滤。流程相关接口会限制在当前空间。

## 映射表单记录

分页，id 升序。

```http
GET /api/v4/mapper/responses?form_id=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "cached_values": {},
    "mapped_values": {},
    "involved_user_ids": [],
    "involved_organization_ids": [],
    "user": {
      "id": 1,
      "name": "示例用户",
      "nickname": "示例",
      "sex": null,
      "phone": "13800138000",
      "identifier": "13800138000",
      "openid": "oEXAMPLE",
      "created_at": "2026-01-01T00:00:00.000+08:00",
      "updated_at": "2026-01-01T00:00:00.000+08:00"
    }
  }
]
```

`GET /api/v4/mapper/responses`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 是 | 表单 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 映射流程

只有 `id`、`title`、`external_settings`。

```http
GET /api/v4/mapper/yaw/flows/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "title": "示例流程",
  "external_settings": {}
}
```

`GET /api/v4/mapper/yaw/flows/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |

## 映射 Journeys

分页。Journey 含 `response`（`cached_values`、`mapped_values`，无 entries）和 Mapper 用户。没有 hourglasses。

```http
GET /api/v4/mapper/yaw/flows/1/journeys?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "sn": "SL202601010001",
    "status": "processing",
    "current_duration_threshold": null,
    "flow_id": 1,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "current_vertex_id": 1,
    "reviewer_vertex_ids": [],
    "journey_url": "https://beta.skylarkly.com/namespaces/1/yet_another_workflow/journeys/1",
    "response": {
      "id": 1,
      "created_at": "2026-01-01T00:00:00.000+08:00",
      "updated_at": "2026-01-01T00:00:00.000+08:00",
      "cached_values": {},
      "mapped_values": {},
      "involved_user_ids": [],
      "involved_organization_ids": [],
      "user": {
        "id": 1,
        "name": "示例用户",
        "phone": "13800138000",
        "identifier": "13800138000"
      }
    },
    "user": {
      "id": 1,
      "name": "示例用户",
      "phone": "13800138000",
      "identifier": "13800138000"
    }
  }
]
```

`GET /api/v4/mapper/yaw/flows/:id/journeys`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

Journey 里的 `response` 复用 Mapper 记录模板，因此带 `user`，没有 `entries`。

## 映射 Assignments

分页。含 Mapper 用户，以及记录的 `id`、时间、`cached_values`、`mapped_values`。

```http
GET /api/v4/mapper/yaw/flows/1/assignments?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "assignee_id": 1,
    "status": "processing",
    "category": "processed",
    "read": false,
    "operation_data": {},
    "current_duration_threshold": null,
    "vertex_id": 1,
    "journey_id": 1,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "user": { "id": 1, "name": "示例用户", "phone": "13800138000" },
    "response": {
      "id": 1,
      "created_at": "2026-01-01T00:00:00.000+08:00",
      "updated_at": "2026-01-01T00:00:00.000+08:00",
      "cached_values": {},
      "mapped_values": {}
    }
  }
]
```

`GET /api/v4/mapper/yaw/flows/:id/assignments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 映射 Moments

分页。

```http
GET /api/v4/mapper/yaw/flows/1/moments?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "status": "processing",
    "comment": null,
    "esignature": null,
    "vertex_id": 1,
    "journey_id": 1,
    "assignment_id": 1,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "user": { "id": 1, "name": "示例用户", "phone": "13800138000" }
  }
]
```

`GET /api/v4/mapper/yaw/flows/:id/moments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 映射 Vertices

分页。只有 `id`、`name`、`type`、`alias_name`。

```http
GET /api/v4/mapper/yaw/flows/1/vertices?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  { "id": 1, "name": "开始", "type": "Vertex::Start", "alias_name": null }
]
```

`GET /api/v4/mapper/yaw/flows/:id/vertices`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |
