# Attachments

`query`、`uptoken`、`base64_file` 需要 `default` scope。`POST /attachments` 与 `POST /attachments/upload` 不校验 JWT。

附件字段见 [Column Explanation](#column-explanation)。`purpose` 目前只能是 `create_responses`。

存储由服务端的写入后端决定。先请求 `uptoken`，再按响应里有没有 `upload_url` 选择上传方式。

## 查询

```http
GET /api/v4/attachments/query?ids[]=1&ids[]=2&fops=&variant= HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

[
  {
    "id": 1,
    "name": "example.png",
    "size": 1024,
    "mime_type": "image/png",
    "extension": "png",
    "extra_info": {},
    "download_url": "https://example.com/attachments/1?signature=placeholder"
  }
]
```

`GET /api/v4/attachments/query`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| ids | integer[] | 是 | 附件 id |
| fops | string | 否 | 传给下载地址的图片处理参数 |
| variant | string | 否 | 传给下载地址的变体名 |

## 获取上传凭证

`user_id` 和 `purpose` 都必填。

七牛等支持表单直传的后端只返回 `uptoken`。其他后端（包括 MinIO）还返回 `upload_url`，指向上面的上传网关。

```http
GET /api/v4/attachments/uptoken?purpose=create_responses&user_id=1 HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

{
  "uptoken": "<upload-token>"
}
```

非表单上传时：

```http
HTTP/1.1 200 OK

{
  "uptoken": "<upload-token>",
  "upload_url": "https://beta.skylarkly.com/api/v4/attachments/upload.json"
}
```

`GET /api/v4/attachments/uptoken`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| purpose | string | 是 | 目前仅 `create_responses`。其他值 422，`errors` 为 `["未知的上传用途"]` |
| user_id | integer | 是 | 附件作者 |

## 上传到七牛

响应里没有 `upload_url` 时，把 `uptoken` 作为表单字段 `token` 发到 `https://up.qbox.me/`。`x:key` 是可选的文件名后缀，不需要固定成某个整数。七牛会按 callback 调用下一节的创建接口，body 为表单字段而不是 JSON：`key`、`name`、`size`、`mime_type`、`user_id`。

```http
POST https://up.qbox.me/ HTTP/1.1
Content-Type: multipart/form-data

token=<uptoken>
file=<binary>
x:key=optional-suffix
```

`POST https://up.qbox.me/`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| token | string | 是 | `uptoken` 返回的凭证 |
| file | file | 是 | 文件 |
| x:key | string | 否 | 文件名后缀 |

## 上传到服务端网关

响应里有 `upload_url` 时，向该地址提交 multipart。这个请求不带 ApiApplication 的 Authorization，凭证在 `token` 里。

```http
POST /api/v4/attachments/upload HTTP/1.1
Content-Type: multipart/form-data

token=<uptoken>
file=<binary>
x:key=optional-suffix
```

成功返回附件 JSON。`token` 无效、缺少 `file` 或超过大小限制时 422，`errors` 为 `["invalid token"]`、`["file required"]` 或 `["文件超过大小限制"]`。

`POST /api/v4/attachments/upload`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| token | string | 是 | `uptoken` 返回的凭证 |
| file | file | 是 | 文件 |
| x:key | string | 否 | 对象名后缀。缺省时用随机 UUID |

## 创建附件

这是七牛 callback，不校验 JWT。成功返回附件 JSON，不是空的 200。

```http
POST /api/v4/attachments HTTP/1.1
Content-Type: application/x-www-form-urlencoded

key=1/create_responses/example-key&name=example.png&size=1024&mime_type=image/png&user_id=1
```

`POST /api/v4/attachments`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| key | string | 是 | 对象键 |
| name | string | 是 | 文件名 |
| size | integer | 是 | 字节数 |
| mime_type | string | 是 | MIME |
| user_id | integer | 是 | 作者 |

## 以 Base64 返回

正文是一个 JSON 字符串，不是对象。路径是附件 id。

```http
GET /api/v4/attachments/1/base64_file HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 200 OK

"aVZCT1J3MEtHZ29BQUFBTlNVaEVVZ0FBQVg="
```

`GET /api/v4/attachments/:id/base64_file`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| id | integer | 是 | 附件 id |
