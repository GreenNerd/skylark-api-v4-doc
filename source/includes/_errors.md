# Errors

失败时的 HTTP 状态和 JSON 形态如下。成功时多数接口返回 200，创建可能是 201，删除和无正文的成功可能是 204 或空的 200。

## 403 与 404

JWT 无效、过期、应用不能访问该空间，或 scope 不足，都是 403。文案是固定的，不包含具体原因。

`appid` 不存在，或按 id 找不到资源，是 404。

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json

{
  "error": "不好意思，你没有权限进行该操作！"
}
```

```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "不好意思，没找到你想要的！"
}
```

## 422

校验失败没有统一外壳，按接口分成下面几种。

模型 `errors` 对象（字段名到消息数组），例如创建用户失败：

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json

{
  "name": ["不能为空"]
}
```

文本数组：

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json

{
  "errors": ["名称不能为空"]
}
```

`errors` 为字符串。表单已关闭时是 `"表单已经关闭"`。微信模板被标记为非法时是 `"模版ID不合法，请登录腾讯后台验证模版ID"`。

组织创建预检失败：

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json

{
  "errors": ["无法找到创建者"]
}
```

流程 `perform` 失败时，正文是执行器自己的 errors。`operation` 为空时是：

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json

{
  "operation": "不能为空"
}
```

## 500

未捕获的异常返回 500。只传 `news_entity`、不传 `template_entity` 的微信推送会在读取模板 id 时出错，属于这种情况。
