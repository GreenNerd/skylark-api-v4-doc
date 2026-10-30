# Comments

列表和创建挂在三个路径上，控制器相同：

- `GET|POST /api/v4/comments`
- `GET|POST /api/v4/forms/:form_id/comments`
- `GET|POST /api/v4/posts/:post_id/comments`

必须能解析出 `form_id`、`post_id`、`cms_page_id`、`template_post_id` 之一。文章和模板帖没有嵌套路由，用 `/api/v4/comments?cms_page_id=` 或 `template_post_id`。

创建、删除需要 `user_id`。列表不需要。评论字段见 [Column Explanation](#column-explanation)。只返回已通过的评论。

## 查询评论

```http
GET /api/v4/comments?form_id=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "author_id": 1,
    "commentable_id": 1,
    "commentable_type": "Form",
    "body": "示例评论",
    "status": "approved",
    "handled_user_id": null,
    "replied_comment_id": null,
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "author": {
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
      "tags": []
    }
  }
]
```

`GET /api/v4/comments`

`GET /api/v4/forms/:form_id/comments`

`GET /api/v4/posts/:post_id/comments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| form_id | integer | 四选一 | 表单。嵌套路径已包含 |
| post_id | integer | 四选一 | 帖子 |
| cms_page_id | integer | 四选一 | 文章 |
| template_post_id | integer | 四选一 | 模板帖 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 新增评论

正文放在 `comment[body]`。成功返回单条评论。

```http
POST /api/v4/comments?form_id=1&user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "comment": {
    "body": "示例评论"
  }
}
```

`POST /api/v4/comments`

`POST /api/v4/forms/:form_id/comments`

`POST /api/v4/posts/:post_id/comments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 作者 |
| comment[body] | string | 是 | 正文 |
| form_id / post_id / cms_page_id / template_post_id | integer | 四选一 | 被评论对象 |

## 单条评论

路由存在，模板也存在，但动作没有加载 `@comment`。当前调用会失败。请使用列表。

`GET /api/v4/comments/:id`

`GET /api/v4/forms/:form_id/comments/:id`

`GET /api/v4/posts/:post_id/comments/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 评论 id |
| form_id | integer | 否 | 嵌套在表单下时的表单 id |
| post_id | integer | 否 | 嵌套在帖子下时的帖子 id |

## 删除评论

只需要 `user_id`。评论必须是该用户写的。不需要 commentable id。

```http
DELETE /api/v4/comments/1?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/comments/:id`

`DELETE /api/v4/forms/:form_id/comments/:id`

`DELETE /api/v4/posts/:post_id/comments/:id`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 评论 id |
| user_id | integer | 是 | 评论作者 |
| form_id | integer | 否 | 嵌套在表单下时的表单 id |
| post_id | integer | 否 | 嵌套在帖子下时的帖子 id |
