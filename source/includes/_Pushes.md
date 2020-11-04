# Pushes

## 微信推送

```http 
POST /api/v4/pushes/wechat HTTP/1.1

```

```http
HTTP/1.1 200 OK
{
  "title":"Happy Day",
  "description":"Is Really A Happy Day",
  "url":"URL",
  "picurl":"PIC_URL"
}

```

### news_entity 结构

结构固定，以下4个key都是必须的，具体意思参考微信[微信客服消息](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421140547)

```http
HTTP/1.1 200 OK
{
  "template_id": "7L5ZG7D0VtqOnKp07bskkJ7XA7veVqIO2VYeY3aYLtY",
  "url": "http://weixin.qq.com/download",
  "data": {
    "first": {
      "value": "恭喜你购买成功！",
      "color": "#173177"
    },
    "keyword1": {
      "value": "巧克力",
      "color": "#173177"
    },
    "keyword2": {
      "value": "39.8元",
      "color": "#173177"
    },
    "remark": {
      "value": "欢迎再次购买！",
      "color": "#173177"
    }
  }
}

```

### template_entity 结构

结构固定，但data的实际结构会根据模板而改变，具体意思参考[微信客服消息](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421140547)

**Parameters**

| Name            | Type   | Description                                                                       |
| --------------- | ------ | --------------------------------------------------------------------------------- |
| openids         | Array  | Required 接收用户的openid的集合                                                   |
| news_entity     | Object | [微信客服消息](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421140547) |
| template_entity | Object | [微信客服消息](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421140547) |

`news_entity`、`template_entity` 两者必须有一个。如果都存在，微信推送会先尝试客服消息，当客服消息失败时，再尝试模板消息

### Response

`Status: 200 OK`

**no body**



## 微信推送（详细版）

```http
POST /api/v4/pushes/wechat HTTP/1.1
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK
参数
{
	"openids": [
		"oXDm5s0XDReFEqbMcAddC_CQGrNY"
	],
	"news_entity": {
		"title": "标题",
		"description": "微信用户与公众号交互后推送此条！",
		"url": "https://www.baidu.com"
	},
	"template_entity": {
		"template_id": "D_p57m-Bj_LRavYckjDwrUb3cU27JkXO0EYUSZy_iqE",
		"url": "https://www.baidu.com",
		"data": {
			"first": {
				"color": "#A94442",
				"value": "【消息】标题"
			},
			"keyword1": {
				"color": "#3C3E49",
				"value": "第一行内容"
			},
			"keyword2": {
				"color": "#3C3E49",
				"value": "第二行内容"
			},
			"remark": {
				"color": "#3C3E49",
				"value": "点击查看详情"
			}
		}
	}
}

```

`POST /api/v4/pushes/wechat`

**Parameters**

| Name            | Type   | Description            | Comments |
| --------------- | ------ | ---------------------- | -------- |
| openids         | string | 用户的openid           |
| news_entity     | object | 用户交互后推送的模板   |
| template_entity | object | 用户未交互后推送的模板 |
| template_id     | string | 空间的模板消息 ID      |
| data            | object | 推送消息的对象结构     |
| url             | string | 推送消息的跳转地址     |


