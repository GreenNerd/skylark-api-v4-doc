# Categories

scope 为 `default`。分类字段：`id`、`name`、`depth`、`description`、`icon`、`position`、`hidden`、`external_link`、`sort_type`、`cms_variables`、`ancestry`、`created_at`。

文章字段：`id`、`title`、`html_body`、`description`、`position`、`external_link`、`cover`、`hidden`、`read_count`、`created_at`、`updated_at`、`attachments`。

## 获取当前空间下所有的分类

分页。

```http
GET /api/v4/categories?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "name": "示例分类",
    "depth": 0,
    "description": null,
    "icon": null,
    "position": 1,
    "hidden": false,
    "external_link": null,
    "sort_type": null,
    "cms_variables": {},
    "ancestry": null,
    "created_at": "2026-01-01T00:00:00.000+08:00"
  }
]
```

`GET /api/v4/categories`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 获取某一个分类

路由和模板都在，但 `find_category` 没有挂在这个动作上，`@category` 为空。当前调用会失败。请用列表或子分类接口。

`GET /api/v4/categories/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 分类 id |

## 创建分类

可写字段在 `cms_category` 下。成功时只设置了 201，没有创建模板，不能依赖 JSON 正文。

```http
POST /api/v4/categories HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "cms_category": {
    "name": "示例分类",
    "parent_id": null,
    "icon": null,
    "description": null,
    "hidden": false,
    "external_link": null,
    "sort_type": null,
    "template_id": null,
    "search_template_id": null,
    "cms_variables": {},
    "admin_ids": "1,2",
    "involved_organization_ids": [],
    "involved_user_tag_ids": []
  }
}
```

`POST /api/v4/categories`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| cms_category[name] | string | 否 | 名称 |
| cms_category[parent_id] | integer | 否 | 上级 |
| cms_category[icon] | string | 否 | 图标 |
| cms_category[description] | string | 否 | 说明 |
| cms_category[hidden] | boolean | 否 | 隐藏 |
| cms_category[external_link] | string | 否 | 外链 |
| cms_category[sort_type] | string | 否 | 排序方式 |
| cms_category[template_id] | integer | 否 | 模板 |
| cms_category[search_template_id] | integer | 否 | 搜索模板 |
| cms_category[cms_variables] | object | 否 | 自定义变量 |
| cms_category[admin_ids] | string | 否 | 逗号分隔的管理员 id，服务端会拆开 |
| cms_category[involved_organization_ids] | integer[] | 否 | 相关组织 |
| cms_category[involved_user_tag_ids] | integer[] | 否 | 相关用户标签 |

## 获取某一个分类下的分类

分页，字段与分类列表相同。

```http
GET /api/v4/categories/1/children?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/categories/:id/children`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 分类 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 获取某一个分类下的文章

分页。

```http
GET /api/v4/categories/1/pages?page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "title": "示例文章",
    "html_body": "<p>正文</p>",
    "description": null,
    "position": 1,
    "external_link": null,
    "cover": null,
    "hidden": false,
    "read_count": 0,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "attachments": []
  }
]
```

`GET /api/v4/categories/:category_id/pages`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| category_id | integer | 是 | 分类 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 文章详情

```http
GET /api/v4/categories/1/pages/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/categories/:category_id/pages/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| category_id | integer | 是 | 分类 id |
| id | integer | 是 | 文章 id |

## 创建文章

成功 201，正文与文章详情相同。

```http
POST /api/v4/categories/1/pages HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "cms_page": {
    "title": "示例文章",
    "cover": null,
    "external_link": null,
    "html_body": "<p>正文</p>",
    "description": null,
    "hidden": false,
    "anonymous": false,
    "template_id": null,
    "comment_status": null,
    "attachment_ids": [],
    "involved_organization_ids": [],
    "involved_user_tag_ids": [],
    "cms_variables": {}
  }
}
```

`POST /api/v4/categories/:category_id/pages`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| category_id | integer | 是 | 分类 id |
| cms_page[title] | string | 否 | 标题 |
| cms_page[cover] | string | 否 | 封面 |
| cms_page[external_link] | string | 否 | 外链 |
| cms_page[html_body] | string | 否 | HTML |
| cms_page[description] | string | 否 | 摘要 |
| cms_page[hidden] | boolean | 否 | 隐藏 |
| cms_page[anonymous] | boolean | 否 | 匿名 |
| cms_page[template_id] | integer | 否 | 模板 |
| cms_page[comment_status] | string | 否 | 评论开关 |
| cms_page[attachment_ids] | integer[] | 否 | 附件 |
| cms_page[involved_organization_ids] | integer[] | 否 | 相关组织 |
| cms_page[involved_user_tag_ids] | integer[] | 否 | 相关用户标签 |
| cms_page[cms_variables] | object | 否 | 自定义变量 |

## 更新文章

```http
PATCH /api/v4/categories/1/pages/1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "cms_page": {
    "title": "示例文章",
    "html_body": "<p>正文</p>"
  }
}
```

`PUT /api/v4/categories/:category_id/pages/:id`

`PATCH /api/v4/categories/:category_id/pages/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| category_id | integer | 是 | 分类 id |
| id | integer | 是 | 文章 id |
| cms_page[title] | string | 否 | 标题 |
| cms_page[cover] | string | 否 | 封面 |
| cms_page[external_link] | string | 否 | 外链 |
| cms_page[html_body] | string | 否 | HTML |
| cms_page[description] | string | 否 | 摘要 |
| cms_page[hidden] | boolean | 否 | 隐藏 |
| cms_page[anonymous] | boolean | 否 | 匿名 |
| cms_page[template_id] | integer | 否 | 模板 |
| cms_page[comment_status] | string | 否 | 评论开关 |
| cms_page[attachment_ids] | integer[] | 否 | 附件 |
| cms_page[involved_organization_ids] | integer[] | 否 | 相关组织 |
| cms_page[involved_user_tag_ids] | integer[] | 否 | 相关用户标签 |
| cms_page[cms_variables] | object | 否 | 自定义变量 |

## 删除文章

```http
DELETE /api/v4/categories/1/pages/1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/categories/:category_id/pages/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| category_id | integer | 是 | 分类 id |
| id | integer | 是 | 文章 id |

## 搜索分类下的文章

`title` 是 PostgreSQL 正则。分页。

```http
GET /api/v4/categories/1/pages/search?title=示例&hidden=false&created_at_gt=2026-01-01&created_at_lt=2026-12-31&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/categories/:category_id/pages/search`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| category_id | integer | 是 | 分类 id |
| title | string | 否 | 标题正则 |
| hidden | boolean | 否 | 是否隐藏 |
| created_at_gt | time | 否 | 创建时间下界 |
| created_at_lt | time | 否 | 创建时间上界 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 文章排序

`positions` 是文章 id 数组，只保留属于该分类的 id。成功是空的 200。

```http
PATCH /api/v4/categories/1/pages/sort HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "positions": [3, 1, 2]
}
```

```http
HTTP/1.1 200 OK
```

`PATCH /api/v4/categories/:category_id/pages/sort`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| category_id | integer | 是 | 分类 id |
| positions | integer[] | 是 | 文章 id，按目标顺序排列 |

## 全空间搜索文章

条件与分类内搜索相同，范围是当前空间的全部文章。

```http
GET /api/v4/pages/all_pages_search?title=示例&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/pages/all_pages_search`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| title | string | 否 | 标题正则 |
| hidden | boolean | 否 | 是否隐藏 |
| created_at_gt | time | 否 | 创建时间下界 |
| created_at_lt | time | 否 | 创建时间上界 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |
