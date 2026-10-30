# CascadedSelects

scope 为 `default`。级联选择含根节点 `choices`。`name` 搜索是 PostgreSQL 正则。

选项字段：`id`、`name`、`ancestry`、`parent_id`、`locked`、`children_count`。`relationships` 只在请求显式要求兄弟或祖先时出现，这两个接口的默认渲染不附带。

## 级联选择详情

```http
GET /api/v4/cascaded_selects/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "name": "示例级联",
  "labels": ["省", "市"],
  "locked": false,
  "min_label_length": 1,
  "choices": [
    {
      "id": 1,
      "name": "示例",
      "ancestry": null,
      "parent_id": null,
      "locked": false,
      "children_count": 0,
      "relationships": {}
    }
  ]
}
```

`GET /api/v4/cascaded_selects/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 级联选择 id |

## 按名称搜索

分页。每条结构与详情相同。

```http
GET /api/v4/cascaded_selects/search?name=示例&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/cascaded_selects/search`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| name | string | 否 | 名称正则。缺省时条件为空，可能匹配异常 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 子节点

```http
GET /api/v4/cascaded_selects/1/choices/1/children HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 2,
    "name": "子项",
    "ancestry": "1",
    "parent_id": 1,
    "locked": false,
    "children_count": 0,
    "relationships": {}
  }
]
```

`GET /api/v4/cascaded_selects/:cascaded_select_id/choices/:id/children`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| cascaded_select_id | integer | 是 | 级联选择 id |
| id | integer | 是 | 选项 id |
