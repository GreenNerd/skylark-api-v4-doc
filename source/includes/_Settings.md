# Settings

scope 为 `manage_organization`。删除是异步的，接口立刻返回 204。

## 批量删除不在任何组织中的成员

```http
DELETE /api/v4/settings/remove_suspended_members HTTP/1.1
Authorization: example-appid:<encoded_data>

```

```http
HTTP/1.1 204 No Content
```

`DELETE /api/v4/settings/remove_suspended_members`
