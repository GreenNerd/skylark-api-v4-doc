# Forms

## 表单信息

```http
GET /api/v4/forms/3987 HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
{
	"id": 7,
	"title": "2016年09月20日工作报告",
	"description": "<p><img src=\"https://images.skylarkly.com/Fh3rPkNswcUh3CCREX_YlfSZnbhI\" alt=\"simditor-img\"><br></p>",
	"created_at": "2016-09-20T16:44:28.082+08:00",
	"updated_at": "2018-08-30T11:33:19.857+08:00",
	"status": "published",
	"fields": [
		{
			"id": 26,
			"title": "为了督促大家填写工作日志，请大家按时完成以下表单！该表单将于明日上午十点关闭。谢谢大家！",
			"description": "",
			"type": "Field::SectionBreak",
			"position": 0,
			"validations": [],
			"other_option": null,
			"visibility": "public_visibility",
			"marked": false,
			"settings": {
				"layout": "block",
				"other_option_settings": {
					"limit": {}
				},
				"length_limit": {},
				"limit_settings": {},
				"char_size_limit_settings": {}
			},
			"detail_id": null,
			"identity_key": "field_26",
			"data": {}
		},
		{
			"id": 27,
			"title": "上午完成工作",
			"description": "",
			"type": "Field::TextArea",
			"position": 3,
			"validations": [
				"presence"
			],
			"other_option": null,
			"visibility": "public_visibility",
			"marked": false,
			"settings": {
				"layout": "block",
				"other_option_settings": {
					"limit": {}
				},
				"length_limit": {},
				"limit_settings": {},
				"char_size_limit_settings": {}
			},
			"detail_id": null,
			"identity_key": "field_27",
			"data": {}
		},
		{
			"id": 28,
			"title": "下午完成工作",
			"description": "",
			"type": "Field::TextArea",
			"position": 4,
			"validations": [
				"presence"
			],
			"other_option": null,
			"visibility": "public_visibility",
			"marked": false,
			"settings": {
				"layout": "block",
				"other_option_settings": {
					"limit": {}
				},
				"length_limit": {},
				"limit_settings": {},
				"char_size_limit_settings": {}
			},
			"detail_id": null,
			"identity_key": "field_28",
			"data": {}
		}
	]
}
```

`GET /api/v4/forms/:id`

**Parameters**

| Name | Type    | Description | Comments |
| ---- | ------- | ----------- | -------- |
| id   | integer | 表单 id     |

## 表单数据

```http
GET /api/v4/forms/548795/responses HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK
X-SLP-Current-Page: 1
X-SLP-Total-Pages: 3
X-SLP-Total-Count: 100
[
	{
		"id": 71630,
		"created_at": "2020-06-18T11:31:53.996+08:00",
		"cached_values": {
			"5924": {
				"value": [
					"test"
				],
				"text_value": [
					"test"
				],
				"exported_value": [
					"test"
				]
			},
			"5925": {
				"value": [
					"12345677654"
				],
				"text_value": [
					"12345677654"
				],
				"exported_value": [
					"12345677654"
				]
			},
			"5926": {
				"value": [
					"2020-06-18 11:28"
				],
				"text_value": [
					"2020-06-18 11:28"
				],
				"exported_value": [
					"2020-06-18 11:28"
				]
			},
			"5927": {
				"value": [
					{
						"id": 6314,
						"gid": "gid://skylark/Option/6314",
						"value": "渠道带访"
					}
				],
				"text_value": [
					"渠道带访"
				],
				"exported_value": [
					"渠道带访"
				]
			}
		},
		"mapped_values": {
			"customer_name": {
				"value": [
					"test"
				],
				"text_value": [
					"test"
				],
				"exported_value": [
					"test"
				]
			},
			"customer_phone": {
				"value": [
					"12345677654"
				],
				"text_value": [
					"12345677654"
				],
				"exported_value": [
					"12345677654"
				]
			},
			"planed_visit_time": {
				"value": [
					"2020-06-18 11:28"
				],
				"text_value": [
					"2020-06-18 11:28"
				],
				"exported_value": [
					"2020-06-18 11:28"
				]
			},
			"customer_source": {
				"value": [
					{
						"id": 6314,
						"gid": "gid://skylark/Option/6314",
						"value": "渠道带访"
					}
				],
				"text_value": [
					"渠道带访"
				],
				"exported_value": [
					"渠道带访"
				]
			}
		},
		"user": {
			"id": 79,
			"name": "樊翔宇",
			"nickname": "左耳朵狗子",
			"sex": 1,
			"phone": "18828072450",
			"identifier": "18828072450",
			"openid": "oXDm5s2v7fnJ2Mut-UiiHtCEIb6Q",
			"created_at": "2017-02-22T13:56:54.125+08:00",
			"updated_at": "2020-06-29T15:50:23.090+08:00",
			"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTKFLWWPT1sSVywib8qpNNfLjMOliblYqa105ibCOKGvzwRV0vAEAlGLcwXkiclCaBcH9leucaTib6Hp95Q/96",
			"tags": [],
			"organizations": [
				{
					"id": 582,
					"name": "lxx",
					"description": null,
					"created_at": "2020-04-08T11:43:40.789+08:00"
				},
				{
					"id": 478,
					"name": "aaaaaaaaaa",
					"description": "",
					"created_at": "2019-05-29T11:50:39.217+08:00"
				},
				{
					"id": 475,
					"name": "二级组织",
					"description": "",
					"created_at": "2019-05-28T17:11:55.970+08:00"
				}
			],
			"profile_submission": {
				"entries": [
					{
						"id": 1091241,
						"field_id": 6035,
						"option_id": null,
						"value": "四川省-成都市-高新区-桂溪街办",
						"choice_id": 7650,
						"value_id": null,
						"latitude": null,
						"longitude": null,
						"group_id": null,
						"detail_id": null
					}
				]
			}
		},
		"entries": [
			{
				"id": 1091207,
				"field_id": 5927,
				"option_id": 6314,
				"value": "渠道带访",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091206,
				"field_id": 5926,
				"option_id": null,
				"value": "2020-06-18 11:28",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091205,
				"field_id": 5925,
				"option_id": null,
				"value": "12345677654",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091204,
				"field_id": 5924,
				"option_id": null,
				"value": "test",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			}
		]
	},
	{
		"id": 71625,
		"created_at": "2020-06-17T16:38:00.775+08:00",
		"cached_values": {
			"5924": {
				"value": [
					"zxl"
				],
				"text_value": [
					"zxl"
				],
				"exported_value": [
					"zxl"
				]
			},
			"5925": {
				"value": [
					"12345678765"
				],
				"text_value": [
					"12345678765"
				],
				"exported_value": [
					"12345678765"
				]
			},
			"5926": {
				"value": [
					"2020-06-17 16:37"
				],
				"text_value": [
					"2020-06-17 16:37"
				],
				"exported_value": [
					"2020-06-17 16:37"
				]
			},
			"5927": {
				"value": [
					{
						"id": 6316,
						"gid": "gid://skylark/Option/6316",
						"value": "电话预约"
					}
				],
				"text_value": [
					"电话预约"
				],
				"exported_value": [
					"电话预约"
				]
			},
			"5928": {
				"value": [
					"未到访"
				],
				"text_value": [
					"未到访"
				],
				"exported_value": [
					"未到访"
				]
			}
		},
		"mapped_values": {
			"customer_name": {
				"value": [
					"zxl"
				],
				"text_value": [
					"zxl"
				],
				"exported_value": [
					"zxl"
				]
			},
			"customer_phone": {
				"value": [
					"12345678765"
				],
				"text_value": [
					"12345678765"
				],
				"exported_value": [
					"12345678765"
				]
			},
			"planed_visit_time": {
				"value": [
					"2020-06-17 16:37"
				],
				"text_value": [
					"2020-06-17 16:37"
				],
				"exported_value": [
					"2020-06-17 16:37"
				]
			},
			"customer_source": {
				"value": [
					{
						"id": 6316,
						"gid": "gid://skylark/Option/6316",
						"value": "电话预约"
					}
				],
				"text_value": [
					"电话预约"
				],
				"exported_value": [
					"电话预约"
				]
			},
			"arrive_visit": {
				"value": [
					"未到访"
				],
				"text_value": [
					"未到访"
				],
				"exported_value": [
					"未到访"
				]
			}
		},
		"user": {
			"id": 1536,
			"name": "希星李",
			"nickname": "希希里图",
			"sex": 1,
			"phone": "18728190482",
			"identifier": "18728190482",
			"openid": null,
			"created_at": "2020-04-08T11:28:36.020+08:00",
			"updated_at": "2020-06-29T15:50:44.783+08:00",
			"headimgurl": "/non-digested-assets/avatars/default_96.png",
			"tags": [],
			"organizations": [
				{
					"id": 582,
					"name": "lxx",
					"description": null,
					"created_at": "2020-04-08T11:43:40.789+08:00"
				},
				{
					"id": 584,
					"name": "xxtest",
					"description": "<p>xxtest</p>",
					"created_at": "2020-04-09T16:15:38.021+08:00"
				}
			],
			"profile_submission": {
				"entries": []
			}
		},
		"entries": [
			{
				"id": 1091199,
				"field_id": 5928,
				"option_id": null,
				"value": "未到访",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091198,
				"field_id": 5927,
				"option_id": 6316,
				"value": "电话预约",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091197,
				"field_id": 5926,
				"option_id": null,
				"value": "2020-06-17 16:37",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091196,
				"field_id": 5925,
				"option_id": null,
				"value": "12345678765",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			},
			{
				"id": 1091195,
				"field_id": 5924,
				"option_id": null,
				"value": "zxl",
				"choice_id": null,
				"value_id": null,
				"latitude": null,
				"longitude": null,
				"group_id": null,
				"detail_id": null
			}
		]
	}
]

```

`GET /api/v4/forms/:id/responses`

**Parameters**

| Name | Type    | Description | Comments |
| ---- | ------- | ----------- | -------- |
| id   | integer | 表单 id     |

## 单条表单数据

```http
GET /api/v4/responses/1385?form=13 HTTP/1.1
Authorization: your_authorization
```

```http
HTTP/1.1 200 OK

{
	"id": 1385,
	"created_at": "2020-08-04T11:23:00.571+08:00",
	"cached_values": {
		"2": {
			"value": [
				"15884559372"
			],
			"text_value": [
				"15884559372"
			],
			"exported_value": [
				"15884559372"
			]
		},
		"4": {
			"value": [
				"杨女士"
			],
			"text_value": [
				"杨女士"
			],
			"exported_value": [
				"杨女士"
			]
		},
		"5": {
			"value": [
				"12121212112"
			],
			"text_value": [
				"12121212112"
			],
			"exported_value": [
				"12121212112"
			]
		},
		"6": {
			"value": [
				{
					"id": 4,
					"gid": "gid://skylark/Option/4",
					"value": "女"
				}
			],
			"text_value": [
				"女"
			],
			"exported_value": [
				"女"
			]
		},
		"7": {
			"value": [
				{
					"id": 534,
					"gid": "gid://skylark/Option/534",
					"value": "小黄车"
				}
			],
			"text_value": [
				"小黄车"
			],
			"exported_value": [
				"小黄车"
			]
		},
		"8": {
			"value": [
				{
					"id": 13,
					"gid": "gid://skylark/Option/13",
					"value": "家庭自住"
				}
			],
			"text_value": [
				"家庭自住"
			],
			"exported_value": [
				"家庭自住"
			]
		},
		"29": {
			"value": [
				{
					"id": 62,
					"gid": "gid://skylark/Option/62",
					"value": "D无意向"
				}
			],
			"text_value": [
				"D无意向"
			],
			"exported_value": [
				"D无意向"
			]
		},
		"71": {
			"value": [
				"一个人到访，说的是给娃娃看房，娃娃在成都工作，然后在外面看了下环境就想走，进来给她讲户型也不是很感兴趣，然后就要慌到走。"
			],
			"text_value": [
				"一个人到访，说的是给娃娃看房，娃娃在成都工作，然后在外面看了下环境就想走，进来给她讲户型也不是很感兴趣，然后就要慌到走。"
			],
			"exported_value": [
				"一个人到访，说的是给娃娃看房，娃娃在成都工作，然后在外面看了下环境就想走，进来给她讲户型也不是很感兴趣，然后就要慌到走。"
			]
		},
		"72": {
			"value": [
				{
					"id": 120,
					"gid": "gid://skylark/Option/120",
					"value": "51-60岁"
				}
			],
			"text_value": [
				"51-60岁"
			],
			"exported_value": [
				"51-60岁"
			]
		},
		"75": {
			"value": [
				{
					"id": 543,
					"gid": "gid://skylark/Option/543",
					"value": "总价61-70万"
				}
			],
			"text_value": [
				"总价61-70万"
			],
			"exported_value": [
				"总价61-70万"
			]
		},
		"76": {
			"value": [
				{
					"id": 126,
					"gid": "gid://skylark/Option/126",
					"value": "按揭"
				}
			],
			"text_value": [
				"按揭"
			],
			"exported_value": [
				"按揭"
			]
		},
		"77": {
			"value": [
				{
					"id": 128,
					"gid": "gid://skylark/Option/128",
					"value": "有"
				}
			],
			"text_value": [
				"有"
			],
			"exported_value": [
				"有"
			]
		},
		"85": {
			"value": [
				"张朦檬"
			],
			"text_value": [
				"张朦檬"
			],
			"exported_value": [
				"张朦檬"
			]
		},
		"152": {
			"value": [
				{
					"id": 2483,
					"gid": "gid://skylark/Choice/2483",
					"value": "四川省-成都市-邛崃市"
				}
			],
			"text_value": [
				"四川省-成都市-邛崃市"
			],
			"exported_value": [
				[
					"四川省",
					"成都市",
					"邛崃市"
				]
			]
		},
		"163": {
			"value": [
				{
					"id": 484,
					"gid": "gid://skylark/Option/484",
					"value": "到访客户"
				}
			],
			"text_value": [
				"到访客户"
			],
			"exported_value": [
				"到访客户"
			]
		},
		"321": {
			"value": [
				{
					"id": 547,
					"gid": "gid://skylark/Option/547",
					"value": "平乐"
				}
			],
			"text_value": [
				"平乐"
			],
			"exported_value": [
				"平乐"
			]
		},
		"322": {
			"value": [
				{
					"id": 554,
					"gid": "gid://skylark/Option/554",
					"value": "区域"
				},
				{
					"id": 555,
					"gid": "gid://skylark/Option/555",
					"value": "地段"
				},
				{
					"id": 556,
					"gid": "gid://skylark/Option/556",
					"value": "户型"
				},
				{
					"id": 557,
					"gid": "gid://skylark/Option/557",
					"value": "装修"
				},
				{
					"id": 558,
					"gid": "gid://skylark/Option/558",
					"value": "价格"
				}
			],
			"text_value": [
				"区域",
				"地段",
				"户型",
				"装修",
				"价格"
			],
			"exported_value": [
				"区域，地段，户型，装修，价格"
			]
		},
		"323": {
			"value": [
				{
					"id": 563,
					"gid": "gid://skylark/Option/563",
					"value": "住宅1F"
				},
				{
					"id": 564,
					"gid": "gid://skylark/Option/564",
					"value": "住宅2F"
				}
			],
			"text_value": [
				"住宅1F",
				"住宅2F"
			],
			"exported_value": [
				"住宅1F，住宅2F"
			]
		},
		"423": {
			"value": [
				{
					"id": 762,
					"gid": "gid://skylark/Option/762",
					"value": "否"
				}
			],
			"text_value": [
				"否"
			],
			"exported_value": [
				"否"
			]
		}
	},
	"mapped_values": {
		"payment_method": {
			"value": [
				{
					"id": 126,
					"gid": "gid://skylark/Option/126",
					"value": "按揭"
				}
			],
			"text_value": [
				"按揭"
			],
			"exported_value": [
				"按揭"
			]
		},
		"saler_phone": {
			"value": [
				"12334566543"
			],
			"text_value": [
				"12334566543"
			],
			"exported_value": [
				"12334566543"
			]
		},
		"customer_gender": {
			"value": [
				{
					"id": 4,
					"gid": "gid://skylark/Option/4",
					"value": "女"
				}
			],
			"text_value": [
				"女"
			],
			"exported_value": [
				"女"
			]
		},
		"customer_phone": {
			"value": [
				"12121212112"
			],
			"text_value": [
				"12121212112"
			],
			"exported_value": [
				"12121212112"
			]
		},
		"customer_name": {
			"value": [
				"杨女士"
			],
			"text_value": [
				"杨女士"
			],
			"exported_value": [
				"杨女士"
			]
		},
		"motivation": {
			"value": [
				{
					"id": 13,
					"gid": "gid://skylark/Option/13",
					"value": "家庭自住"
				}
			],
			"text_value": [
				"家庭自住"
			],
			"exported_value": [
				"家庭自住"
			]
		},
		"channel": {
			"value": [
				{
					"id": 534,
					"gid": "gid://skylark/Option/534",
					"value": "小黄车"
				}
			],
			"text_value": [
				"小黄车"
			],
			"exported_value": [
				"小黄车"
			]
		},
		"working_area": {
			"value": [
				{
					"id": 2483,
					"gid": "gid://skylark/Choice/2483",
					"value": "四川省-成都市-邛崃市"
				}
			],
			"text_value": [
				"四川省-成都市-邛崃市"
			],
			"exported_value": [
				[
					"四川省",
					"成都市",
					"邛崃市"
				]
			]
		},
		"age": {
			"value": [
				{
					"id": 120,
					"gid": "gid://skylark/Option/120",
					"value": "51-60岁"
				}
			],
			"text_value": [
				"51-60岁"
			],
			"exported_value": [
				"51-60岁"
			]
		},
		"saler": {
			"value": [
				"张朦檬"
			],
			"text_value": [
				"张朦檬"
			],
			"exported_value": [
				"张朦檬"
			]
		},
		"intention": {
			"value": [
				{
					"id": 62,
					"gid": "gid://skylark/Option/62",
					"value": "D无意向"
				}
			],
			"text_value": [
				"D无意向"
			],
			"exported_value": [
				"D无意向"
			]
		},
		"living_area2": {
			"value": [
				{
					"id": 547,
					"gid": "gid://skylark/Option/547",
					"value": "平乐"
				}
			],
			"text_value": [
				"平乐"
			],
			"exported_value": [
				"平乐"
			]
		},
		"entitlement": {
			"value": [
				{
					"id": 128,
					"gid": "gid://skylark/Option/128",
					"value": "有"
				}
			],
			"text_value": [
				"有"
			],
			"exported_value": [
				"有"
			]
		},
		"remark": {
			"value": [
				"一个人到访，说的是给娃娃看房，娃娃在成都工作，然后在外面看了下环境就想走，进来给她讲户型也不是很感兴趣，然后就要慌到走。"
			],
			"text_value": [
				"一个人到访，说的是给娃娃看房，娃娃在成都工作，然后在外面看了下环境就想走，进来给她讲户型也不是很感兴趣，然后就要慌到走。"
			],
			"exported_value": [
				"一个人到访，说的是给娃娃看房，娃娃在成都工作，然后在外面看了下环境就想走，进来给她讲户型也不是很感兴趣，然后就要慌到走。"
			]
		},
		"source": {
			"value": [
				{
					"id": 484,
					"gid": "gid://skylark/Option/484",
					"value": "到访客户"
				}
			],
			"text_value": [
				"到访客户"
			],
			"exported_value": [
				"到访客户"
			]
		},
		"customer_resistance": {
			"value": [
				{
					"id": 554,
					"gid": "gid://skylark/Option/554",
					"value": "区域"
				},
				{
					"id": 555,
					"gid": "gid://skylark/Option/555",
					"value": "地段"
				},
				{
					"id": 556,
					"gid": "gid://skylark/Option/556",
					"value": "户型"
				},
				{
					"id": 557,
					"gid": "gid://skylark/Option/557",
					"value": "装修"
				},
				{
					"id": 558,
					"gid": "gid://skylark/Option/558",
					"value": "价格"
				}
			],
			"text_value": [
				"区域",
				"地段",
				"户型",
				"装修",
				"价格"
			],
			"exported_value": [
				"区域，地段，户型，装修，价格"
			]
		},
		"preferred_apartment": {
			"value": [
				{
					"id": 563,
					"gid": "gid://skylark/Option/563",
					"value": "住宅1F"
				},
				{
					"id": 564,
					"gid": "gid://skylark/Option/564",
					"value": "住宅2F"
				}
			],
			"text_value": [
				"住宅1F",
				"住宅2F"
			],
			"exported_value": [
				"住宅1F，住宅2F"
			]
		},
		"price_range": {
			"value": [
				{
					"id": 543,
					"gid": "gid://skylark/Option/543",
					"value": "总价61-70万"
				}
			],
			"text_value": [
				"总价61-70万"
			],
			"exported_value": [
				"总价61-70万"
			]
		},
		"line_card": {
			"value": [
				{
					"id": 762,
					"gid": "gid://skylark/Option/762",
					"value": "否"
				}
			],
			"text_value": [
				"否"
			],
			"exported_value": [
				"否"
			]
		}
	},
	"involved_user_ids": [],
	"involved_organization_ids": [],
	"entries": [
		{
			"id": 10584,
			"field_id": 423,
			"option_id": 762,
			"value": "否",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10583,
			"field_id": 163,
			"option_id": 484,
			"value": "到访客户",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10180,
			"field_id": 2,
			"option_id": null,
			"value": "15884559372",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10179,
			"field_id": 85,
			"option_id": null,
			"value": "张朦檬",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10178,
			"field_id": 321,
			"option_id": 547,
			"value": "平乐",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10177,
			"field_id": 152,
			"option_id": null,
			"value": "四川省-成都市-邛崃市",
			"choice_id": 2483,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10176,
			"field_id": 322,
			"option_id": 558,
			"value": "价格",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10175,
			"field_id": 322,
			"option_id": 557,
			"value": "装修",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10174,
			"field_id": 322,
			"option_id": 555,
			"value": "地段",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10173,
			"field_id": 322,
			"option_id": 556,
			"value": "户型",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10172,
			"field_id": 322,
			"option_id": 554,
			"value": "区域",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10171,
			"field_id": 76,
			"option_id": 126,
			"value": "按揭",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10170,
			"field_id": 75,
			"option_id": 543,
			"value": "总价61-70万",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10169,
			"field_id": 323,
			"option_id": 563,
			"value": "住宅1F",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10168,
			"field_id": 323,
			"option_id": 564,
			"value": "住宅2F",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10167,
			"field_id": 8,
			"option_id": 13,
			"value": "家庭自住",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10166,
			"field_id": 7,
			"option_id": 534,
			"value": "小黄车",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10165,
			"field_id": 29,
			"option_id": 62,
			"value": "D无意向",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10164,
			"field_id": 77,
			"option_id": 128,
			"value": "有",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10163,
			"field_id": 72,
			"option_id": 120,
			"value": "51-60岁",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10162,
			"field_id": 71,
			"option_id": null,
			"value": "一个人到访，说的是给娃娃看房，娃娃在成都工作，然后在外面看了下环境就想走，进来给她讲户型也不是很感兴趣，然后就要慌到走。",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10161,
			"field_id": 6,
			"option_id": 4,
			"value": "女",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10160,
			"field_id": 5,
			"option_id": null,
			"value": "12121212112",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 10159,
			"field_id": 4,
			"option_id": null,
			"value": "杨女士",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		}
	],
	"user": {
		"id": 75,
		"name": "张朦檬",
		"nickname": "Smile",
		"sex": 2,
		"phone": "15884559372",
		"identifier": "15884559372",
		"openid": "ouvMN1qTZ_ucaufm5HFI26w_Q43A",
		"created_at": "2020-07-03T10:17:37.855+08:00",
		"updated_at": "2020-07-03T11:13:04.931+08:00",
		"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/AAlQYG92O3xBbrZniaa6uv6ex5wTeUyllIKYu7zWwrqrCvoL9jCuic21P7sGR52r1WjgsCxMic5kSzwiahz5JClxbQ/96",
		"tags": [
			{
				"id": 2,
				"name": "magnate_saler"
			},
			{
				"id": 1,
				"name": "magnate_admin"
			}
		],
		"organizations": [
			{
				"id": 8,
				"name": "销售",
				"description": "",
				"created_at": "2020-07-03T10:17:02.093+08:00"
			}
		]
	}
}

```

`GET /api/v4/responses/:dataID`

**Parameters**

| Name   | Type    | Description | Comments |
| ------ | ------- | ----------- | -------- |
| dataID | integer | 数据 id     |

## 创建表单填写记录

```http
POST /api/v4/forms/:form_id/responses HTTP/1.1
Authorization: your_authorization

body中传入:
{
    "response": {
		"entries_attributes": [
			{
				"field_id": 5888,
				"value": "zxl"
			},
			{
				"field_id": 5890,
				"value": "12345677654"
			}
		]
	},
	"user_id": "690"
}
```

```http
HTTP/1.1 201 OK
{
	"id": 71657,
	"created_at": "2020-07-06T14:30:57.219+08:00",
	"cached_values": {
		"5888": {
			"value": [
				"zxl"
			],
			"text_value": [
				"zxl"
			],
			"exported_value": [
				"zxl"
			]
		},
		"5890": {
			"value": [
				"12345677654"
			],
			"text_value": [
				"12345677654"
			],
			"exported_value": [
				"12345677654"
			]
		}
	},
	"mapped_values": {
		"customer_phone": {
			"value": [
				"zxl"
			],
			"text_value": [
				"zxl"
			],
			"exported_value": [
				"zxl"
			]
		},
		"is_new": {
			"value": [
				"12345677654"
			],
			"text_value": [
				"12345677654"
			],
			"exported_value": [
				"12345677654"
			]
		}
	},
	"involved_user_ids": [],
	"involved_organization_ids": [],
	"entries": [
		{
			"id": 1091336,
			"field_id": 5888,
			"option_id": null,
			"value": "zxl",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 1091337,
			"field_id": 5890,
			"option_id": null,
			"value": "12345677654",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		}
	],
	"user": {
		"id": 690,
		"name": "zxl",
		"nickname": "贤独丨🤺",
		"sex": 1,
		"phone": "12345677654",
		"identifier": "12345677654",
		"openid": "oXDm5s0XDReFEqbMcAddC_CQGrNY",
		"created_at": "2019-12-30T11:20:05.128+08:00",
		"updated_at": "2020-07-06T11:07:48.147+08:00",
		"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/KU6FI52PPicLT6iaZ88S49btibcTic2OcnSg4gObibYyxc92giafHRwjpNgaPZKRiaRGt47sdoulxO3fqzdn69EjmyTwQ/96",
		"tags": [],
		"organizations": [],
		"profile_submission": {
			"entries": []
		}
	}
}
```

`POST /api/v4/forms/:form_id/responses`

**Parameters**

| Name     | Type    | Description | Comments |
| -------- | ------- | ----------- | -------- |
| form_id  | integer | 表单 id     |
| field_id | integer | 选项 id     |
| value    | string  | 选项值      |
| user_id  | integer | 用户 id     |

## 修改表单填写记录

```http
PUT /api/v4/forms/:form_id/responses/:id HTTP/1.1
Authorization: your_authorization

```

```http
HTTP/1.1 200 OK

body中：
{
	"response": {
		"entries_attributes": [
			{
				"id": 1091336,
				"value": "zxl"
			},
			{
				"id": 1091337,
				"value": "111"
			}
		]
	}
}


{
	"id": 71657,
	"created_at": "2020-07-06T14:30:57.219+08:00",
	"cached_values": {
		"5888": {
			"value": [
				"12121"
			],
			"text_value": [
				"12121"
			],
			"exported_value": [
				"12121"
			]
		},
		"5890": {
			"value": [
				"124534"
			],
			"text_value": [
				"124534"
			],
			"exported_value": [
				"124534"
			]
		}
	},
	"mapped_values": {
		"customer_phone": {
			"value": [
				"12121"
			],
			"text_value": [
				"12121"
			],
			"exported_value": [
				"12121"
			]
		},
		"is_new": {
			"value": [
				"124534"
			],
			"text_value": [
				"124534"
			],
			"exported_value": [
				"124534"
			]
		}
	},
	"involved_user_ids": [],
	"involved_organization_ids": [],
	"entries": [
		{
			"id": 1091336,
			"field_id": 5888,
			"option_id": null,
			"value": "12121",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		},
		{
			"id": 1091337,
			"field_id": 5890,
			"option_id": null,
			"value": "124534",
			"choice_id": null,
			"value_id": null,
			"latitude": null,
			"longitude": null,
			"group_id": null,
			"detail_id": null
		}
	],
	"user": {
		"id": 690,
		"name": "zxl",
		"nickname": "贤独丨🤺",
		"sex": 1,
		"phone": "12345677654",
		"identifier": "12345677654",
		"openid": "oXDm5s0XDReFEqbMcAddC_CQGrNY",
		"created_at": "2019-12-30T11:20:05.128+08:00",
		"updated_at": "2020-07-06T11:07:48.147+08:00",
		"headimgurl": "http://thirdwx.qlogo.cn/mmopen/vi_32/KU6FI52PPicLT6iaZ88S49btibcTic2OcnSg4gObibYyxc92giafHRwjpNgaPZKRiaRGt47sdoulxO3fqzdn69EjmyTwQ/96",
		"tags": [],
		"organizations": [],
		"profile_submission": {
			"entries": []
		}
	}
}
```

`PUT /api/v4/forms/:form_id/responses/:id`

**Parameters**

| Name      | Type    | Description               | Comments |
| --------- | ------- | ------------------------- | -------- |
| :form_id  | integer | 表单 id                   |
| :id       | integer | 修改用数据 id             |
| :field_id | integer | 如果没有值则则用 field_id |
