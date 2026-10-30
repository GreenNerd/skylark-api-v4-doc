# Posts

scope 为 `default`。评论见 [Comments](#comments)。

## 创建帖子

成功返回帖子 JSON。作者对象是后台用户模板。

```http
POST /api/v4/posts HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "post": {
    "title": "示例帖子",
    "html_body": "<p>正文</p>",
    "status": "published",
    "enable_appendable": false,
    "published_as_id": null,
    "namecard_id": null,
    "comment_status": null,
    "tag_ids": [1],
    "cloned_from_id": null,
    "author_id": 1,
    "attachment_ids": [],
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
      "total_num": 1,
      "_destroy": false
    },
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
    }
  }
}
```

```http
HTTP/1.1 200 OK

{
  "id": 1,
  "title": "示例帖子",
  "html_body": "<p>正文</p>",
  "created_at": "2026-01-01T00:00:00.000+08:00",
  "glanceable": null,
  "cloned_from_id": null,
  "body": "正文",
  "tag_ids": [1],
  "tags": [],
  "attachments": []
}
```

`POST /api/v4/posts`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| post[title] | string | 否 | 标题 |
| post[html_body] | string | 否 | HTML 正文 |
| post[status] | string | 否 | 状态 |
| post[enable_appendable] | boolean | 否 | 允许追加 |
| post[published_as_id] | integer | 否 | 发布身份 |
| post[namecard_id] | integer | 否 | 名片 |
| post[comment_status] | string | 否 | 评论开关 |
| post[tag_ids] | integer[] | 否 | 标签 |
| post[cloned_from_id] | integer | 否 | 复制来源 |
| post[author_id] | integer | 否 | 作者 |
| post[attachment_ids] | integer[] | 否 | 附件 |
| post[red_packet_setting_attributes] | object | 否 | `_destroy`、`wishing`、`act_name`、`remark`、`send_name`、`per_amount`、`begin_per_amount`、`end_per_amount`、`expired_at`、`random`、`total_num` |
| post[user_boundary_attributes] | object | 否 | 见 Column Explanation |
| post[push_agent_on_publish_attributes] | object | 否 | `include_uncompleted`、`push_package_id`、`scheduled_at` |

响应里的 `author` 和 `user_boundary` 使用后台模板，字段比 v4 用户更多。`body` 是截断到 50 字的纯文本。
