# ImportRecords

scope 为 `import_records`。`user_id` 必填。

`type` 只能是下面五个类名。`ImportRecord::CreateResponses` 还要通过 `form_id` 找到表单，其他四个的导入对象是当前空间。

- `ImportRecord::BulkUpdateUsers`
- `ImportRecord::OrganizationMembers`
- `ImportRecord::CreateCascadedSelect`
- `ImportRecord::Users`
- `ImportRecord::CreateResponses`

## 导入记录列表

分页，按 id 降序。

```http
GET /api/v4/import_records?type=ImportRecord::Users&user_id=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "user_id": 1,
    "status": "processing",
    "file": null,
    "recordable_id": 1,
    "recordable_type": "Namespace",
    "options": {},
    "type": "ImportRecord::Users",
    "failure": null,
    "success": null,
    "original_filename": "users.xlsx",
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00"
  }
]
```

`GET /api/v4/import_records`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| type | string | 是 | 上面五个类名之一 |
| user_id | integer | 是 | 当前空间的用户 |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 创建导入记录

先用附件接口上传文件，再把 `attachment_id` 传进来。成功正文只有 `{ "is_async": true }`，不是导入记录本身。

```http
POST /api/v4/import_records?user_id=1&attachment_id=1&form_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>
Content-Type: application/json

{
  "import_record": {
    "type": "ImportRecord::Users",
    "file": null,
    "options": {}
  }
}
```

```http
HTTP/1.1 200 OK

{
  "is_async": true
}
```

`POST /api/v4/import_records`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 操作者 |
| attachment_id | integer | 是 | 已上传的附件 |
| form_id | integer | 条件 | `type` 为 `ImportRecord::CreateResponses` 时必填 |
| import_record[type] | string | 是 | 五个类名之一 |
| import_record[file] | string | 否 | 可传，文件名以附件为准 |
| import_record[options] | object | 否 | 导入选项 |
