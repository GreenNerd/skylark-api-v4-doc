# Accesses

## 获取权限ID

```http
GET /api/v4/accesses
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK
[
	{
		"id": 1,
		"name": "超级管理员",
		"actions": [
			1,
			3,
			4
		],
		"founded": false
	},
	{
		"id": 16,
		"name": "发送消息、表单和模板通知",
		"actions": [
			4
		],
		"founded": false
	},
	{
		"id": 17,
		"name": "管理组织架构",
		"actions": [
			1
		],
		"founded": false
	},
	{
		"id": 18,
		"name": "管理组织成员",
		"actions": [
			3
		],
		"founded": false
	},
	{
		"id": 26,
		"name": "组织管理员",
		"actions": [
			1,
			3
		],
		"founded": false
	}
]
```

`GET /api/v4/accesses`


## 创建组织管理员

```http
GET /api/v4/organizations/:organization_id/administrators?user_id&access_id
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK
{
	"id": 320,
	"user": {
		"id": 690,
		"name": "zxl",
		"nickname": "贤丨🤺",
		"phone": "12121212121",
		"identifier": "12121212121",
		"qq": null,
		"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/KU6FI52PPicLT6iaZ88S49btibcTic2OcnSg4gObibYyxc92giafHRwjpNgaPZKRiaRGt47sdoulxO3fqzdn69EjmyTwQ",
		"openid": "oXDm5s0XDReFEqbMcAddC_CQGrNY",
		"imported_alias": "zxl",
		"from_wechat": false,
		"tags": [],
		"profile_submission": {
			"entries": []
		}
	},
	"access": {
		"id": 1,
		"name": "超级管理员",
		"actions": [
			1,
			3,
			4
		],
		"founded": false
	},
	"organization": {
		"id": 590,
		"name": "111111",
		"description": "",
		"created_at": "2020-05-13T11:37:02.061+08:00"
	}
}
```

`POST /api/v4/organizations/:organization_id/administrators?user_id&access_id`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| user_id | integer | 用户ID |
| access_id | integer | 权限ID |
| :organization_id | integer | 组织ID |


## 删除组织管理员

```http
DELETE /api/v4/organizations/:organization_id/administrators/:id
Authorization: your_authorization
```

```http
HTTP/1.1 204 OK

```

`DELETE /api/v4/organizations/:organization_id/administrators/:id`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| :id | integer | 管理员ID |
| :organization_id | integer | 组织ID |


## 修改组织管理员

```http
PUT /api/v4/organizations/:organization_id/administrators:id
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK
{
	"id": 321,
	"user": {
		"id": 690,
		"name": "zxl",
		"nickname": "贤丨🤺",
		"phone": "12123456654",
		"identifier": "12123456654",
		"qq": null,
		"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/KU6FI52PPicLT6iaZ88S49btibcTic2OcnSg4gObibYyxc92giafHRwjpNgaPZKRiaRGt47sdoulxO3fqzdn69EjmyTwQ",
		"openid": "oXDm5s0XDReFEqbMcAddC_CQGrNY",
		"imported_alias": "zxl",
		"from_wechat": false,
		"tags": [],
		"profile_submission": {
			"entries": []
		}
	},
	"access": {
		"id": 18,
		"name": "管理组织成员",
		"actions": [
			3
		],
		"founded": false
	},
	"organization": {
		"id": 590,
		"name": "111111",
		"description": "",
		"created_at": "2020-05-13T11:37:02.061+08:00"
	}
}

```

`PUT /api/v4/organizations/:organization_id/administrators:id`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| user_id | integer | 用户ID |
| access_id | integer | 权限ID |
| :id | integer | 管理员ID |
| :organization_id | integer | 组织ID |


## 查询每个组织下的管理员

```http
GET /api/v4/organizations/:organization_id/administrators
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK
[
	{
		"id": 311,
		"user": {
			"id": 1536,
			"name": "希星李",
			"nickname": "希希里图",
			"phone": "12345677654",
			"identifier": "12345677654",
			"qq": "",
			"headimgurl": "/non-digested-assets/avatars/default.png",
			"openid": null,
			"imported_alias": "lxx",
			"from_wechat": false,
			"tags": [],
			"profile_submission": {
				"entries": []
			}
		},
		"access": {
			"id": 2,
			"name": "创建者",
			"actions": [
				1,
				3,
				4
			],
			"founded": true
		},
		"organization": {
			"id": 590,
			"name": "111111",
			"description": "",
			"created_at": "2020-05-13T11:37:02.061+08:00"
		}
	},
	{
		"id": 319,
		"user": {
			"id": 194,
			"name": "zx",
			"nickname": "",
			"phone": "12345677654",
			"identifier": "字符串",
			"qq": "",
			"headimgurl": "/non-digested-assets/avatars/default.png",
			"openid": null,
			"imported_alias": "张瑞",
			"from_wechat": false,
			"tags": [],
			"profile_submission": {
				"entries": []
			}
		},
		"access": {
			"id": 18,
			"name": "管理组织成员",
			"actions": [
				3
			],
			"founded": false
		},
		"organization": {
			"id": 590,
			"name": "111111",
			"description": "",
			"created_at": "2020-05-13T11:37:02.061+08:00"
		}
	},
	{
		"id": 321,
		"user": {
			"id": 690,
			"name": "zxl",
			"nickname": "贤独丨🤺",
			"phone": "12345677654",
			"identifier": "12345677654",
			"qq": null,
			"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/KU6FI52PPicLT6iaZ88S49btibcTic2OcnSg4gObibYyxc92giafHRwjpNgaPZKRiaRGt47sdoulxO3fqzdn69EjmyTwQ",
			"openid": "oXDm5s0XDReFEqbMcAddC_CQGrNY",
			"imported_alias": "zxl",
			"from_wechat": false,
			"tags": [],
			"profile_submission": {
				"entries": []
			}
		},
		"access": {
			"id": 1,
			"name": "超级管理员",
			"actions": [
				1,
				3,
				4
			],
			"founded": false
		},
		"organization": {
			"id": 590,
			"name": "111111",
			"description": "",
			"created_at": "2020-05-13T11:37:02.061+08:00"
		}
	}
]

```

`Get /api/v4/organizations/:organization_id/administrators`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| :organization_id | integer | 组织ID |

