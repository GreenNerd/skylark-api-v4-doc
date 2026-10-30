---
title: API Reference

language_tabs:
  - http

toc_footers:


includes:
  - Pagination
  - errors
  - ColumnExplanation
  - WechatClient
  - Pushes
  - Users
  - Organizations
  - Tags
  - Accesses
  - Settings
  - Forms
  - Posts
  - Comments
  - Attachments
  - Categories
  - CascadedSelects
  - IdentityCertifications
  - VerifyCodes
  - ImportRecords
  - ExportableFiles
  - RedPackets
  - Flows
  - Mapper

search: true
---

# Introduction

Welcome to the Skylark API!

域名：

  - 测试：https://beta.skylarkly.com
  - 正式：https://skylarkly.com

**注**：

  - 对接在测试环境完成。下文示例里的 `Authorization` 使用本节算出的 `example-appid:<encoded_data>`
  - 除特别声明外，请求体为 JSON，`Content-Type: application/json`
  - 更新接口同时接受 `PUT` 和 `PATCH`
  - 列表接口的分页见 [Pagination](#pagination)

# Authentication

接口使用 ApiApplication 的 `appid` 与 `appsecret`。应用还必须被授权访问目标空间，并且 `scopes` 包含该接口要求的 scope。

## 请求头

`Authorization` 的形式是 `appid:encoded_data`，中间只有一个冒号。

`encoded_data` 是用 `appsecret` 做密钥的 JWT，算法 `HS256`。代码只读取 payload 里的 `namespace_id`（整数）。如果 payload 带了 `exp`，过期后 ruby-jwt 会拒绝该令牌。

示例凭证（假值，可在 [jwt.io](https://jwt.io) 用同一密钥验签）：

`appid: example-appid`

`appsecret: example-appsecret`

`namespace_id: 1`

HEADER：`{"typ":"JWT","alg":"HS256"}`

PAYLOAD：`{"namespace_id":1}`

`encoded_data`：

`eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lc3BhY2VfaWQiOjF9.gd-ziDMMbtTqXiBHs8gOnXRjoDgPuqx0wR-lv8fcXcY`

`Authorization`：

`example-appid:eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lc3BhY2VfaWQiOjF9.gd-ziDMMbtTqXiBHs8gOnXRjoDgPuqx0wR-lv8fcXcY`

带过期时间的 payload：`{"namespace_id":1,"exp":1893456000}`

对应 `encoded_data`：

`eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lc3BhY2VfaWQiOjEsImV4cCI6MTg5MzQ1NjAwMH0.JZzCNMa3NlU5FCyHStT-wlGSad0EqedRb6cgwFW_jgs`

## Scope

| scope | 用在 |
| --- | --- |
| `default` | 未单独声明的接口 |
| `organization_user` | 读取、更新、删除组织，以及 `GET /organizations/:id/members` |
| `manage_organization` | `POST /organizations`、组织成员的增删改与搜索、组织管理员、权限列表、清理挂起成员 |
| `push` | 微信推送 |
| `wechat_client` | access_token 与 jsapi_ticket |
| `identity_certifications` | 人脸核身 |
| `user_login_token` | 签发用户登录令牌。还要求配置打开 `v4.login.enable` |
| `verify_code` | 短信验证码 |
| `import_records` | 导入记录 |
| `red_packet` | 发红包 |

`namespace_ids` 包含 `0` 时，该应用可以访问全部空间。

## 不校验 JWT 的请求

- `OPTIONS /api/v4/*` 是 CORS 预检，直接返回 200
- `POST /api/v4/attachments` 与 `POST /api/v4/attachments/upload` 跳过 JWT。上传凭证在 `uptoken` 步骤签发

CORS 允许的方法：`POST, GET, PUT, PATCH, DELETE, OPTIONS`。
