# Users

## 查询当前空间下所有用户
```http
GET /api/v4/users HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
[
  {
    "id": 1,
    "name": "第一个管理员",
    "nickname": "",
    "phone": "1111111111",
    "identifier": "1111111111",
    "qq": "123",
    "headimgurl": "/non-digested-assets/avatars/default.png",
    "openid": "123",
    "imported_alias": "第一个管理员",
    "from_wechat": false,
    "tags": [{
      "id": 1,
      "name": "b1",
      "full_name": "bq-b1",
      "color": "#e91e63",
      "tag_group_id": 1,
      "taggings_count": 9
    }, {
      "id": 3,
      "name": "a1",
      "full_name": "a1",
      "color": "#ff5722",
      "tag_group_id": 1,
      "taggings_count": 4
    }, {
      "id": 8,
      "name": "a2",
      "full_name": "a2",
      "color": "#673ab7",
      "tag_group_id": 1,
      "taggings_count": 1
    }
	},
  {
    "id": 1,
    "name": "第二个管理员",
    "nickname": "",
    "phone": "12222222222",
    "identifier": "12222222222",
    "qq": "123",
    "headimgurl": "/non-digested-assets/avatars/default.png",
    "openid": "123",
    "imported_alias": "第一个管理员",
    "from_wechat": false,
    "tags": [{
      "id": 1,
      "name": "b1",
      "full_name": "bq-b1",
      "color": "#e91e63",
      "tag_group_id": 1,
      "taggings_count": 9
    }, {
      "id": 3,
      "name": "a1",
      "full_name": "a1",
      "color": "#ff5722",
      "tag_group_id": 1,
      "taggings_count": 4
    }, {
      "id": 8,
      "name": "a2",
      "full_name": "a2",
      "color": "#673ab7",
      "tag_group_id": 1,
      "taggings_count": 1
    }
  }
]
```

`GET /api/v4/users`

## 所在组织

```http
GET /api/v4/users/14473/organizations HTTP/1.1
Authorization: your_authorization
{
  "name": "name",
  "description": "description",
  "application_strategy": "must_approved",
  "founder_id": 3,
  "patent_id": 13
}

```

```http
HTTP/1.1 200 OK
[
  {
    "id": 14473,
    "name": "child_1",
    "description": "",
    "description_text": "",
    "created_at": "2017-04-18T16:33:07.408+08:00",
    "updated_at": "2017-12-06T17:52:27.556+08:00",
    "children_count": 1,
    "parent_id": 14472,
    "ancestry": "14472"
  },
  {
    "id": 1935,
    "name": "测试组织",
    "description": "<p>aaa</p>",
    "description_text": "aaa",
    "created_at": "2015-05-25T15:58:45.083+08:00",
    "updated_at": "2018-04-06T15:37:24.712+08:00",
    "children_count": 2,
    "parent_id": null,
    "ancestry": null
  },
  ...
]
```

`GET /api/v4/users/:id/organizations`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| id | integer | 用户id |


## 查询用户信息

```http
GET /api/v4/users/1 HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
{
  "id": 1,
  "name": "第一个管理员",
  "nickname": "",
  "phone": "1111111111",
  "identifier": "1111111111",
  "qq": "123",
  "headimgurl": "/non-digested-assets/avatars/default.png",
  "openid": "123",
  "imported_alias": "第一个管理员",
  "from_wechat": false,
  "tags": [{
    "id": 1,
    "name": "b1",
    "full_name": "bq-b1",
    "color": "#e91e63",
    "tag_group_id": 1,
    "taggings_count": 9
  }, {
    "id": 3,
    "name": "a1",
    "full_name": "a1",
    "color": "#ff5722",
    "tag_group_id": 1,
    "taggings_count": 4
  }, {
    "id": 8,
    "name": "a2",
    "full_name": "a2",
    "color": "#673ab7",
    "tag_group_id": 1,
    "taggings_count": 1
  }
}
```

`GET /api/v4/users/:id`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| id | integer | 用户id |


## 新建用户信息

```http
POST /api/v4/users HTTP/1.1
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK
{
	"id": 115,
	"name": "zxl",
	"nickname": null,
	"sex": null,
	"phone": "11011011011",
	"identifier": "77777",
	"openid": null,
	"created_at": "2020-06-19T14:52:48.240+08:00",
	"updated_at": "2020-06-19T14:52:48.240+08:00",
	"headimgurl": "/non-digested-assets/avatars/default_96.png",
	"tags": [],
	"organizations": []
}
```


`POST /api/v4/users`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| name | string | 名字 |
| identifier | string | 识别码 |
| phone | integer | 手机号 |


## 更新用户信息

自定义字段：先在 空间设置-->用户属性设置 中添加

```http
PUT /api/v4/users/:id HTTP/1.1
Authorization: your_authorization
在 body 中
{
    "profile_submission_attributes": {
        "entries_attributes": [
            {
                "field_id": 5980,
                "value": "数据"
            },
            {
                "field_id": 5977,
                "value": "二号数据"
            },
            {
                "field_id": 5976,
                "value": "新数据"
            },
            {
                "field_id": 5974,
                "value": "四号数据"
            }
        ]
    }
}
```


```http
HTTP/1.1 200 OK
{
	"id": 323,
	"name": "望天wangtian",
	"nickname": null,
	"sex": null,
	"phone": "186000000000",
	"identifier": "186000000000",
	"openid": null,
	"created_at": "2018-10-11T14:55:21.550+08:00",
	"updated_at": "2018-10-11T14:55:21.550+08:00",
	"headimgurl": "/non-digested-assets/avatars/default_96.png",
	"tags": [],
	"organizations": [
		{
			"id": 409,
			"name": "11",
			"description": "",
			"created_at": "2018-10-15T18:09:13.526+08:00"
		}
	],
	"profile_submission": {
		"entries": [
			{
				"id": 1091215,
				"field_id": 5980,
				"option_id": null,
				"value": "23",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091216,
				"field_id": 5977,
				"option_id": null,
				"value": "23123",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091217,
				"field_id": 5976,
				"option_id": null,
				"value": "测34试",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091218,
				"field_id": 5974,
				"option_id": null,
				"value": "454",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			}
		]
	}
}
```


`PUT /api/v4/users/:id`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| name | string | 名字 |
| identifier | string | 识别码 |
| phone | integer | 手机号 |
| profile_submission_attributes | object | 自定义对象 |
| id | integer | 如果已有自定义属性，那么就用id修改 |
| fieldf_id | integer | 当没有属性的时候用fieldf_id创建 |





## 查询用户信息（手机号）

```http
GET /api/v4/users/query HTTP/1.1
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK
{
  "id": 115,
  "name": "zxl",
  "nickname": null,
  "sex": null,
  "phone": "11011011011",
  "identifier": "77777",
  "openid": null,
  "created_at": "2020-06-19T14:52:48.240+08:00",
  "updated_at": "2020-06-19T14:52:48.240+08:00",
  "headimgurl": "/non-digested-assets/avatars/default_96.png",
  "tags": [],
  "organizations": []
}
```

`GET /api/v4/users/query`

**Parameters**

| Name | Type | Description | Comments |
| --- | --- | --- | ---- |
| keyword | integer | 手机号 |


