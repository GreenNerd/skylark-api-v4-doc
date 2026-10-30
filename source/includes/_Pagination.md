# Pagination

使用分页的列表接受：

- `page`：页码，从 1 开始
- `per_page`：每页条数，默认 `24`，最大 `100`

响应头：

- `X-SLP-Current-Page`：当前页
- `X-SLP-Total-Pages`：总页数
- `X-SLP-Total-Count`：总条数

```http
GET /api/v4/yaw/flows/1/journeys?per_page=30&page=3 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

`GET /api/v4/yaw/flows/:flow_id/journeys` 在带 `query` 搜索时，总条数按搜索结果计算，不是对全表 `count(*)`。

`GET /api/v4/tags` 调用了分页，但没有使用分页后的集合。响应头可能是某一页的数字，正文仍是全部标签。
