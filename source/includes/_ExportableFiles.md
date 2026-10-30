# Exportable files

scope 为 `default`。表单导出和流程导出创建的文件从这里取。`user_id` 必填，只能看到该用户自己的文件。

## 导出文件列表

可按导出对象过滤。分页，按 id 降序。

```http
GET /api/v4/exportable_files?user_id=1&exportable_type=Form&exportable_id=1&page=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "exportable_id": 1,
    "exportable_type": "Form",
    "file": "export.xlsx",
    "type": "ExportableFile::ResponseableResponses",
    "created_at": "2026-01-01T00:00:00.000+08:00",
    "updated_at": "2026-01-01T00:00:00.000+08:00",
    "status": "finished",
    "options": {},
    "user_id": 1,
    "size": 1024,
    "full_filename": "export.xlsx"
  }
]
```

`GET /api/v4/exportable_files`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| user_id | integer | 是 | 文件所属用户 |
| exportable_type | string | 否 | 与 `exportable_id` 一起用 |
| exportable_id | integer | 否 | 来源对象 id |
| page | integer | 否 | 页码 |
| per_page | integer | 否 | 每页条数 |

## 下载地址

```http
GET /api/v4/exportable_files/1/download?user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "download_url": "https://example.com/exports/1?signature=placeholder"
}
```

`GET /api/v4/exportable_files/:id/download`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 导出文件 id |
| user_id | integer | 是 | 文件所属用户 |
