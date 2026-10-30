# Flows

scope 为 `default`。对象字段见 [Column Explanation](#column-explanation)。发起和审批成功时返回的是后台任务模板，不是本节列表里的 v4 Journey。

`GET /api/v4/yaw/flows/:id` 支持 `slim=1`，此时省略 `vertices`、`edges`、`graphs`。这个详情按 id 查找，没有按当前空间过滤。同组的其他流程接口会限制在当前空间。

## 用户可见的流程

`user_id` 必填。返回的是计数缓存，不是流程详情。

```http
GET /api/v4/yaw/flows?user_id=1&flow_id=1&category=processed&completed=0&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "user_id": 1,
    "flow_id": 1,
    "flow_title": "示例流程",
    "proposed_uncompleted_assignments_count": 0,
    "processed_uncompleted_assignments_count": 1,
    "cc_uncompleted_assignments_count": 0,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00"
  }
]
```

`GET /api/v4/yaw/flows`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 当前空间的用户 |
| flow_id | integer | 否 | 限定流程 |
| category | string | 否 | `processed`、`proposed`、`cc` |
| completed | string | 否 | 传给任务过滤器 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 获取流程详情

```http
GET /api/v4/yaw/flows/1?slim=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "title": "示例流程",
  "html_body": "<p>说明</p>",
  "external_settings": {},
  "identity_vertify_type": null,
  "logic_settings": {},
  "fields": []
}
```

不带 `slim` 时还有 `vertices`、`edges`、`graphs`。节点名称字段是 `name`。

`GET /api/v4/yaw/flows/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| slim | string | 否 | 传 `1` 时省略 `vertices`、`edges`、`graphs` |

## 更新流程

`user_id` 必填，记为修改人。`PUT` 与 `PATCH` 都可以。成功返回流程详情。流程 `status` 为 `composing`、`active`、`archived`、`blocked`。`fields_attributes` 见 Column Explanation。

```http
PATCH /api/v4/yaw/flows/1?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "flow": {
    "title": "示例流程",
    "html_body": "<p>说明</p>",
    "sn_prefix": "SL",
    "status": "active",
    "identity_vertify_type": null,
    "identity_vertify_notice": null,
    "showed_in_dash": true,
    "enable_custom_sn": false,
    "propose_after_journey_ended": false,
    "notify_proposer_after_journey_ended": false,
    "after_submit_action": null,
    "after_submit_redirect_url": null,
    "external_settings": {},
    "cover": { "icon": null, "bgcolor": null },
    "tag_ids": [],
    "fields_attributes": [],
    "serial_number_fields_attributes": [
      {
        "id": 1,
        "type_name": "const",
        "position": 1,
        "_destroy": false,
        "settings": {
          "rule": null,
          "proposer_attribute": null,
          "field_id": null,
          "const_text": "SL"
        }
      }
    ],
    "settings": { "marked_field_ids": [] },
    "logic_settings": {}
  }
}
```

`PUT /api/v4/yaw/flows/:id`

`PATCH /api/v4/yaw/flows/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| user_id | integer | 是 | 修改人 |
| flow[title] | string | 否 | 标题 |
| flow[html_body] | string | 否 | 说明 |
| flow[sn_prefix] | string | 否 | 单号前缀 |
| flow[status] | string | 否 | `composing`、`active`、`archived`、`blocked` |
| flow[identity_vertify_type] | string | 否 | 实名校验类型 |
| flow[identity_vertify_notice] | string | 否 | 实名校验提示 |
| flow[showed_in_dash] | boolean | 否 | 是否出现在工作台 |
| flow[enable_custom_sn] | boolean | 否 | 是否自定义单号 |
| flow[propose_after_journey_ended] | boolean | 否 | 结束后仍可发起 |
| flow[notify_proposer_after_journey_ended] | boolean | 否 | 结束后通知发起人 |
| flow[after_submit_action] | string | 否 | 提交后动作 |
| flow[after_submit_redirect_url] | string | 否 | 提交后跳转地址 |
| flow[external_settings] | object | 否 | 外部设置 |
| flow[cover] | object | 否 | `icon`、`bgcolor` |
| flow[tag_ids] | integer[] | 否 | 标签 |
| flow[fields_attributes] | object[] | 否 | 见 Column Explanation |
| flow[serial_number_fields_attributes] | object[] | 否 | 单号片段 |
| flow[settings] | object | 否 | 含 `marked_field_ids` |
| flow[logic_settings] | object | 否 | 出现时整段放行，不走字段白名单 |

`logic_settings` 在 `flow` 里出现时整段放行，不走字段白名单。

## 查询流程单号对应的 id

响应是对象。签名路径是 `journey_ids`。

```http
GET /api/v4/yaw/flows/1/journey_ids HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "journey_ids": [1]
}
```

`GET /api/v4/yaw/flows/:id/journey_ids`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |

## 流程下的任务

分页，v4 Assignment。

```http
GET /api/v4/yaw/flows/1/assignments?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:id/assignments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 流程下的 Moment

查询条件写成了 `deleted_at = null`。在 SQL 里这永远不成立，这个列表当前会是空的。请改用某条 journey 下的 moments。

`GET /api/v4/yaw/flows/:id/moments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |

## 某个用户的任务

`user_id` 必填。`completed` 默认 `"0"`。可按 `flow_id`、`vertex_id`、`category` 过滤。`journey_query` 的键见 Column Explanation 的 journey 搜索。分页。返回 v4 Assignment。

```http
GET /api/v4/yaw/flows/user_assignments?user_id=1&flow_id=1&vertex_id=1&category=processed&completed=0&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/user_assignments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 任务所属用户 |
| completed | string | 否 | 默认 `0` |
| flow_id | integer | 否 | 流程 |
| vertex_id | integer | 否 | 节点 |
| category | string | 否 | `processed`、`proposed`、`cc` |
| journey_query | object | 否 | 需同时有 `flow_id` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 某个用户在流程上的 Journey

不传 `category` 时按 `processed`（数值 0）。`status` 是任务状态名。分页。返回 Journey 列表。

```http
GET /api/v4/yaw/flows/1/user_journeys?user_id=1&category=proposed&status=processing&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:id/user_journeys`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 流程 id |
| user_id | integer | 是 | 任务处理人 |
| category | string | 否 | 缺省为 `processed` |
| status | string | 否 | 任务状态 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 当前用户已处理的任务

`user_id` 必填。`status` 默认 `processing`。分页。

```http
GET /api/v4/yaw/flows/1/assignments/processed?user_id=1&status=processing&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/assignments/processed`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| user_id | integer | 是 | 当前用户 |
| status | string | 否 | 默认 `processing` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 节点详情

```http
GET /api/v4/yaw/flows/1/vertices/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/vertices/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| id | integer | 是 | 节点 id |

# Journeys

## 获取发起的流程任务列表

不含暂存。分页，id 升序。

```http
GET /api/v4/yaw/flows/1/journeys?page=1&per_page=24 HTTP/1.1
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
      "cached_values": {},
      "mapped_values": {},
      "entries": []
    },
    "user": {
      "id": 1,
      "name": "示例用户",
      "phone": "13800138000",
      "identifier": "13800138000"
    },
    "hourglasses": []
  }
]
```

`GET /api/v4/yaw/flows/:flow_id/journeys`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 读取暂存

返回暂存中的 Journey，并附带它的 `assignments`。没有暂存时 404。

```http
GET /api/v4/yaw/flows/1/journeys/new?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys/new`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| user_id | integer | 是 | 发起人 |

## 单条 Journey

```http
GET /api/v4/yaw/flows/1/journeys/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| id | integer | 是 | Journey id |

## 按单号查找

```http
GET /api/v4/yaw/flows/1/journeys/find_by_sn?sn=SL202601010001 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys/find_by_sn`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| sn | string | 是 | 单号 |

找不到时不会 404，后续渲染可能失败。请先确认单号存在。

## 获取某个用户发起的流程

返回 Journey 数组，不是 Assignment。

```http
GET /api/v4/yaw/flows/1/journeys/proposed_journeys?user_id=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys/proposed_journeys`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| user_id | integer | 是 | 发起人 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 搜索 Journey

`query` 的键见 Column Explanation。带 `query` 时总条数不是简单计数。

```http
GET /api/v4/yaw/flows/1/journeys/search?query[-5]=SL202601010001&query[-6]=processing&query[-8]=开始&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys/search`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| query | object | 否 | 键见 Column Explanation |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 导出 Journey

`user_id` 必填。成功是空的 201。文件从导出文件接口下载。

```http
POST /api/v4/yaw/flows/1/journeys/export?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "options": {}
}
```

```http
HTTP/1.1 201 Created
```

`POST /api/v4/yaw/flows/:flow_id/journeys/export`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| user_id | integer | 是 | 导出人 |
| options | object | 否 | 导出选项 |

## 更新 Journey 状态

只接受 `journey[status]`。成功是空的 200。

```http
PATCH /api/v4/yaw/flows/1/journeys/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "journey": {
    "status": "aborted"
  }
}
```

```http
HTTP/1.1 200 OK
```

`PUT /api/v4/yaw/flows/:flow_id/journeys/:id`

`PATCH /api/v4/yaw/flows/:flow_id/journeys/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| id | integer | 是 | Journey id |
| journey[status] | string | 是 | 流程任务状态 |

## 当前处理人

返回精简用户数组。

```http
GET /api/v4/yaw/flows/1/journeys/1/current_processing_users HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys/:id/current_processing_users`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| id | integer | 是 | Journey id |

## 当前 Moment

返回单条 Moment。没有处理中的 moment 时对象为空。

```http
GET /api/v4/yaw/flows/1/journeys/1/processing_moment HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys/:id/processing_moment`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| id | integer | 是 | Journey id |

## 删除暂存

只删除暂存状态的 journey。无论是否找到，都返回 204。

```http
DELETE /api/v4/yaw/flows/1/journeys/1/destroy_stashed_journey HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/yaw/flows/:flow_id/journeys/:id/destroy_stashed_journey`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| id | integer | 是 | Journey id |

## 创建流程任务

`user_id` 必填。操作放在 `assignment[operation]`，不是顶层字段。

发起人可用的 `operation`：

| operation | 会保留的字段 |
| --- | --- |
| route | `operation`、`response_attributes`。还可带 webhook |
| stash | `operation`、`response_attributes` |
| propose | `operation`、`next_vertex_id`、`next_reviewer_ids`、`duration_thresholds`、`carbon_copy_user_ids`、`esignature` |
| cancel | 只保留 `operation` |
| remind | 不裁剪，控制器允许的字段都会传入 |

`route` 且 `webhook.subscribed_events` 包含 `JourneyStatusChangeEvent` 时，才会给这条 journey 创建 webhook。

`route` 的成功体是 `{ assignment, next_vertices, next_graphs }`。其他操作的成功体是后台 Assignment 对象。失败见 [Errors](#errors)。

```http
POST /api/v4/yaw/flows/1/journeys?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "user_id": 1,
  "assignment": {
    "operation": "propose",
    "esignature": null,
    "comment": "同意",
    "transfer_to_user_id": null,
    "next_vertex_id": 2,
    "next_reviewer_ids": [1],
    "carbon_copy_user_ids": [],
    "duration_thresholds": [{ "gid": "gid://example/Vertex/2", "value": "P1D" }],
    "response_attributes": {
      "entries_attributes": [
        {
          "id": null,
          "_destroy": false,
          "field_id": 1,
          "value": "示例",
          "option_id": null,
          "choice_id": null,
          "value_id": null,
          "longitude": null,
          "latitude": null,
          "group_id": null
        }
      ]
    }
  },
  "webhook": {
    "payload_url": "https://example.com/hooks",
    "subscribed_events": ["JourneyStatusChangeEvent"]
  }
}
```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "status": "processing",
  "category": "proposed",
  "read": false,
  "current_duration_threshold": null,
  "created_at": "2026-01-01T00:00:00.000+08:00",
  "updated_at": "2026-01-01T00:00:00.000+08:00",
  "after_submit_action": null,
  "after_submit_redirect_url": null,
  "gid": "gid://skylark/YetAnotherWorkflow::Assignment/1",
  "pretty_current_duration_threshold": null,
  "journey": {
    "id": 1,
    "sn": "SL202601010001",
    "custom_sn": null,
    "status": "processing"
  },
  "response": null
}
```

`operation` 为 `route` 时：

```http
HTTP/1.1 200 OK

{
  "assignment": { "id": 1, "status": "processing", "category": "proposed" },
  "next_vertices": [
    { "id": 2, "name": "审批", "type": "Vertex::Normal", "gid": "gid://skylark/YetAnotherWorkflow::Vertex/2" }
  ],
  "next_graphs": [
    { "id": 1, "name": "主流程", "gid": "gid://skylark/YetAnotherWorkflow::Graph/1" }
  ]
}
```

`POST /api/v4/yaw/flows/:flow_id/journeys`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| flow_id | integer | 是 | 流程 id |
| user_id | integer | 是 | 发起人 |
| assignment[operation] | string | 是 | `route`、`stash`、`propose`、`cancel`、`remind` |
| assignment[response_attributes] | object | 否 | 含 `entries_attributes` |
| assignment[next_vertex_id] | integer | 否 | 下一节点 |
| assignment[next_reviewer_ids] | integer[] | 否 | 下一处理人 |
| assignment[duration_thresholds] | object[] | 否 | `gid`、`value` |
| assignment[carbon_copy_user_ids] | integer[] | 否 | 抄送用户 |
| assignment[esignature] | string | 否 | 签名 |
| assignment[comment] | string | 否 | 意见 |
| assignment[transfer_to_user_id] | integer | 否 | 转交用户 |
| webhook[payload_url] | string | 否 | `route` 时的回调地址 |
| webhook[subscribed_events] | string[] | 否 | 含 `JourneyStatusChangeEvent` 才创建 webhook |

# Assignments

列表、详情和按节点查询都在 journey 下面。处理任务的路径也在 journey 下面，但处理人用 `user_id` 查找，任务必须属于该用户。

## 任务列表

```http
GET /api/v4/yaw/journeys/1/assignments?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/journeys/:journey_id/assignments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 任务详情

```http
GET /api/v4/yaw/journeys/1/assignments/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/journeys/:journey_id/assignments/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| id | integer | 是 | 任务 id |

## 按节点查询

```http
GET /api/v4/yaw/journeys/1/assignments/query_by_vertex_id?vertex_id=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/journeys/:journey_id/assignments/query_by_vertex_id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| vertex_id | integer | 是 | 节点 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 处理任务

`user_id` 必填。任务若是发起人任务，走发起人操作：`route`、`stash`、`propose`、`cancel`、`remind`。否则走审批人操作：

| operation | 会保留的字段 |
| --- | --- |
| route | `operation`、`comment`、`esignature`、`response_attributes` |
| approve | 再加上 `next_vertex_id`、`next_reviewer_ids`、`duration_thresholds`、`carbon_copy_user_ids` |
| refuse | `operation`、`comment`、`esignature`、`carbon_copy_user_ids`、`response_attributes`、`refuse_to_vertex_id`、`refuse_to_reviewer_ids` |
| transfer | `operation`、`comment`、`esignature`、`transfer_to_user_id`、`carbon_copy_user_ids` |

成功体与创建 journey 相同。

```http
PATCH /api/v4/yaw/journeys/1/assignments/1?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "assignment": {
    "operation": "approve",
    "comment": "同意",
    "esignature": null,
    "next_vertex_id": 3,
    "next_reviewer_ids": [2],
    "refuse_to_vertex_id": null,
    "refuse_to_reviewer_ids": [],
    "transfer_to_user_id": null,
    "carbon_copy_user_ids": [],
    "duration_thresholds": [],
    "response_attributes": {
      "entries_attributes": []
    }
  }
}
```

`PUT /api/v4/yaw/journeys/:journey_id/assignments/:id`

`PATCH /api/v4/yaw/journeys/:journey_id/assignments/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| id | integer | 是 | 任务 id |
| user_id | integer | 是 | 处理人 |
| assignment[operation] | string | 是 | 发起人或审批人操作，见上文 |
| assignment[comment] | string | 否 | 意见 |
| assignment[esignature] | string | 否 | 签名 |
| assignment[response_attributes] | object | 否 | 含 `entries_attributes` |
| assignment[next_vertex_id] | integer | 否 | 下一节点 |
| assignment[next_reviewer_ids] | integer[] | 否 | 下一处理人 |
| assignment[duration_thresholds] | object[] | 否 | `gid`、`value` |
| assignment[carbon_copy_user_ids] | integer[] | 否 | 抄送用户 |
| assignment[refuse_to_vertex_id] | integer | 否 | 退回节点 |
| assignment[refuse_to_reviewer_ids] | integer[] | 否 | 退回处理人 |
| assignment[transfer_to_user_id] | integer | 否 | 转交用户 |

# Moments

路径里的 id 是 journey id，不是流程 id。

## 获取某条流程任务的所有 Moment

分页，id 升序。

```http
GET /api/v4/yaw/journeys/1/moments?page=1 HTTP/1.1
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
    "flow_id": 1,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "assignment": null,
    "user": null
  }
]
```

`GET /api/v4/yaw/journeys/:journey_id/moments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 更新 Moment

只接受 `status` 和 `comment`。

```http
PATCH /api/v4/yaw/journeys/1/moments/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "moment": {
    "status": "approved",
    "comment": "同意"
  }
}
```

`PUT /api/v4/yaw/journeys/:journey_id/moments/:id`

`PATCH /api/v4/yaw/journeys/:journey_id/moments/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| id | integer | 是 | Moment id |
| moment[status] | string | 否 | 状态 |
| moment[comment] | string | 否 | 意见 |

# Hourglasses

可选 `status`。分页。字段见 Column Explanation。

```http
GET /api/v4/yaw/journeys/1/hourglasses?status=counting&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/journeys/:journey_id/hourglasses`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| status | string | 否 | 计时器状态，如 `counting` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

# Delay requests

字段见 Column Explanation。

## Journey 下的列表

```http
GET /api/v4/yaw/journeys/1/delay_requests?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/journeys/:journey_id/delay_requests`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| journey_id | integer | 是 | Journey id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 创建延期申请

`user_id` 必填。任务必须属于该用户。

```http
POST /api/v4/yaw/assignments/1/delay_requests?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "delay_request": {
    "assignment_id": 2,
    "hourglass_id": 1,
    "data": { "message": "需要延期" }
  }
}
```

`POST /api/v4/yaw/assignments/:assignment_id/delay_requests`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| assignment_id | integer | 是 | 任务 id |
| user_id | integer | 是 | 申请人 |
| delay_request[assignment_id] | integer | 否 | 被延期的任务 |
| delay_request[hourglass_id] | integer | 否 | 计时器 |
| delay_request[data][message] | string | 否 | 申请说明 |

## 处理延期

更新时会把新的 `data` 合并进原有 `data`。

```http
PATCH /api/v4/yaw/delay_requests/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "delay_request": {
    "status": "approved",
    "data": {
      "reply": "同意",
      "duration_threshold_value": "P2D"
    }
  }
}
```

`PUT /api/v4/yaw/delay_requests/:id`

`PATCH /api/v4/yaw/delay_requests/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 延期申请 id |
| delay_request[status] | string | 否 | 如 `approved` |
| delay_request[data][reply] | string | 否 | 回复，合并进原有 `data` |
| delay_request[data][duration_threshold_value] | string | 否 | 新的时限，如 `P2D` |

## 我处理的延期

`status` 默认 `processing`。`user_id` 是任务处理人。

```http
GET /api/v4/yaw/delay_requests/processed_delay_requests?user_id=1&flow_id=1&status=processing&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/delay_requests/processed_delay_requests`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 处理人 |
| flow_id | integer | 是 | 流程 |
| status | string | 否 | 默认 `processing` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 我发起的延期

按申请人的任务过滤。

```http
GET /api/v4/yaw/delay_requests/requested_delay_requests?user_id=1&flow_id=1&status=processing&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/delay_requests/requested_delay_requests`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 申请人 |
| flow_id | integer | 是 | 流程 |
| status | string | 否 | 默认 `processing` |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |
