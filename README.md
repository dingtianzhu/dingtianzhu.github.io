# Wash
一个跳火洗护多功能平台的一部分，主要是洗护

# 接口文档
* 公共用到的全局参数
* 除登陆接口，其他接口均须带header头授权验证


|全局url|默认请求方式|成功返回状态|失败返回状态|
|----------|---------|---------|---------|
|https://test.tosneaker.com/api/ | POST|200|500|

### 订单状态号和对应的意义

|订单状态号|0|1|2|3|4|5|6|7|8|
|-------|-|-|-|-|-|-|-|-|-|
|对应的含义|带录入|待审核|待处理|已完成|待结算|待退回：不可修复|待退回：不用修复|已结算|已退回|


## 小程序登陆接口
* 请求接口`/app/login`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|mobile|string:len:11|是|用户手机号|
|password|string:min:6max:16|是|用户密码|

返回值
```
{
	"access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczovL3Rlc3QudG9zbmVha2VyLmNvbS9hcGkvYXBwL2xvZ2luIiwiaWF0IjoxNTYzMTU3MjY5LCJleHAiOjE1NjMxNjA4NjksIm5iZiI6MTU2MzE1NzI2OSwianRpIjoiV0hJMnBZWGF6U1MzemVtVSIsInN1YiI6MjUsInBydiI6IjUxODNjNmY5NzJiNDUwMDEzMzA3ZTI2OGJhODlhMjcxMzNhYjg2YjgiLCJyb2xlIjoidXNlciJ9.8AkAm6dz1ZLlwlI3TyRsUlq_BljcsDu0E1un4-oNf0g",
	"token_type": "bearer",
	"expires_in": 3600
}
```

## 小程序获取信息接口
* 请求接口`/auth/me`
* 请求方式：默认

返回值
```
{
	"id": 25,
	"username": "辅导费",
	"password": "$2y$10$/wEUG9sv7cgYMYp.eH2CcOdB5HfVqSLnoe/kPS1T62vXOpfLB6Xxq",
	"type": 2,
	"mobile": "15733036829",
	"quota": "30.00",
	"owner_id": 1,
	"remember_token": null,
	"created_at": "2019-07-13 15:25:13",
	"updated_at": "2019-07-13 15:25:13",
	"deleted_at": null
}
```

# 检查端接口文档

## 寄售商请求列表
* 请求接口`/auth/consign`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|登陆检查员id|


返回值
```
[
	{
		"id": 25,
		"username": "辅导费",
		"password": "$2y$10$/wEUG9sv7cgYMYp.eH2CcOdB5HfVqSLnoe/kPS1T62vXOpfLB6Xxq",
		"type": 2,
		"mobile": "15733036829",
		"quota": "30.00",
		"owner_id": 1,
		"remember_token": null,
		"created_at": "2019-07-13 15:25:13",
		"updated_at": "2019-07-13 15:25:13",
		"deleted_at": null
	},
	{
		"id": 29,
		"username": "测试寄售商",
		"password": "$2y$10$ZnhNb2XW8QjlL/TFysSAremoNtFpaFtbx5SYU/UGtwCuh1W5ylEvu",
		"type": 2,
		"mobile": "18603532471",
		"quota": "10.00",
		"owner_id": 1,
		"remember_token": null,
		"created_at": "2019-07-15 07:47:01",
		"updated_at": "2019-07-15 07:47:01",
		"deleted_at": null
	}
]
```

## 获取qiniu token
* 请求接口`/auth/getQiniuToken`
* 请求方式：默认

返回值
```
PRQ6YEFwh3jWh-2a2IduBRxpOX3QVXRoCFFAH7XT:kFAFzIAYdKXVPHgIw8P84DOzSFo=:eyJzY29wZSI6InRvc25lYWtlci1jb20iLCJkZWFkbGluZSI6MTU2MzE2Mjk5N30=
```

## 订单添加
* 请求接口`/auth/order`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|consignor_id|int|是|寄售商id|
|bai_id|string|是|条形码号|
|original_image|array|是|瑕疵图片|


返回值
```
{
	"message": "添加成功",
	"status": 200
}
```

# 寄售端接口文档

## 订单添加
* 请求接口`/auth/orderList`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|states|int|是|订单状态号[1,2,3,5,6,8]|
|page|int|否|页码|

返回值
```
{
	"data": [
		{
			"id": 40,
			"consignor_id": 29,
			"bar_id": "66666",
			"original_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/88cd9c3f4c60e75.jpg\"]",
			"end_image": null,
			"states": 2,
			"price": "11111.00",
			"tab_ids": ",17,",
			"scheme": "测试 ￥11111.00*1",
			"compant": null,
			"code": null,
			"created_at": "2019-07-13 18:26:25",
			"updated_at": "2019-07-13 18:26:25",
			"deleted_at": null,
			"wash_id": 0
		}
	],
	"count": 1
}
```

## 修改订单状态
* 请求接口`/auth/setStates`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|ids|array|是|订单id数组|
|consignor_id|int|是|寄售商ID|
|states|int|是|要改到的状态|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

## 设置审核额度值
* 请求接口`/auth/setQuota`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|寄售商ID|
|quota|decimal(10,2)|是|要设置额度|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

## 通过快递号获取订单列表
* 请求接口`/auth/getOrders`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|code|string|是|快递单号|
|page|int|否|当前页码|

返回值
```
	"data": [
		{
			"id": 39,
			"consignor_id": 29,
			"bar_id": "000000",
			"original_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/b699ae3def39a56.jpg\"]",
			"end_image": null,
			"states": 8,
			"price": "11111.00",
			"tab_ids": ",15,",
			"scheme": "测试 ￥11111.00*1",
			"compant": "顺丰",
			"code": "0000001",
			"created_at": "2019-07-15 08:19:34",
			"updated_at": "2019-07-15 08:19:34",
			"deleted_at": null,
			"wash_id": 0
		}
	],
	"count": 1
}
```

# 洗护端接口文档

## 获取Tab列表
* 请求接口`/auth/washTab`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|owner_id|int|是|商户ID|
|page|int|否|页码|
|pageSize|int|否|页面大小|

返回值
```
{
	"data": [
		{
			"id": 8,
			"title": "清洗",
			"price": "12.00",
			"is_show": 1,
			"owner_id": 1,
			"order_id": null,
			"created_at": "2019-07-13 15:32:30",
			"updated_at": "2019-07-13 15:32:30",
			"deleted_at": null,
			"count": 0
		},

	],
	"count": 1
}
```

## 获取具体Tab下的Order列表
* 请求接口`/auth/washLists`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|Tab标签ID|
|page|int|否|页码|
|pageSize|int|否|页面大小|

返回值
```
{
	"data": [
		{
			"id": 59,
			"consignor_id": 29,
			"bar_id": "262622",
			"original_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/eaf48e948f40997.jpg\"]",
			"end_image": null,
			"states": 2,
			"price": "10.00",
			"tab_ids": ",10,",
			"scheme": "测试项目 ￥10.00*1",
			"compant": null,
			"code": null,
			"created_at": "2019-07-15 07:50:26",
			"updated_at": "2019-07-15 07:50:26",
			"deleted_at": null,
			"wash_id": 0
		},
		{
			"id": 68,
			"consignor_id": 29,
			"bar_id": "000007",
			"original_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/3acfdd415125060.jpg\"]",
			"end_image": null,
			"states": 2,
			"price": "10.00",
			"tab_ids": ",10,",
			"scheme": "测试项目 ￥10.00*1",
			"compant": null,
			"code": null,
			"created_at": "2019-07-15 07:50:12",
			"updated_at": "2019-07-15 07:50:12",
			"deleted_at": null,
			"wash_id": 0
		}
	],
	"count": 2
}
```

## 清洗完提交接口
* 请求接口`/auth/setDone`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|订单ID|
|end_image|array|是|处理完成图片|
|wash_id|int|是|清洗员id|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

## 获取具体处理完成的Order列表
* 请求接口`/auth/getDone`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|清洗员ID|
|page|int|否|页码|
|pageSize|int|否|页面大小|

返回值
```
{
	"data": [
		{
			"id": 34,
			"consignor_id": 25,
			"bar_id": "122222",
			"original_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/c7cab1d7565d2a9.jpg\"]",
			"end_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/ebcbe68786350ec.jpg\"]",
			"states": 3,
			"price": "130.00",
			"tab_ids": ",9,10,",
			"scheme": "补色 ￥120.00*1 测试项目 ￥10.00*1",
			"compant": null,
			"code": null,
			"created_at": "2019-07-13 18:33:57",
			"updated_at": "2019-07-13 18:33:57",
			"deleted_at": null,
			"wash_id": 30
		},
	],
	"count": 1
}
```

# 服务端接口文档

## 获取带录入的订单列表
* 请求接口`/auth/orderLists`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|page|int|否|页码|
|pageSize|int|否|页面大小|

返回值
```
{
	"0": {
		"id": 33,
		"consignor_id": 25,
		"bar_id": "31221",
		"original_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/o6zAJs2D_mGZKOP5KF_kEYpMJTQk.xzky8NSfxz5z0b703e02d\",\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/o6zAJs2D_mGZKOP5KF_kEYpMJTQk.BM9hLaJnNQPO83ffb971a\"]",
		"end_image": null,
		"states": 0,
		"price": "0.00",
		"tab_ids": null,
		"scheme": null,
		"compant": null,
		"code": null,
		"created_at": "2019-07-13 15:15:44",
		"updated_at": "2019-07-13 15:15:44",
		"deleted_at": null,
		"wash_id": 0
	},
	"count": 1
}
```

## 获取商户下所有标签Tab接口
* 请求接口`/auth/tabList`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|owner_id|int|是|商户ID|
|page|int|否|页码|
|pageSize|int|否|页面大小|
|search|string|否|搜索内容|

返回值
```
{
	"data": [
		{
			"id": 8,
			"title": "清洗",
			"price": "12.00",
			"is_show": 1,
			"owner_id": 1,
			"order_id": null,
			"created_at": "2019-07-13 15:32:30",
			"updated_at": "2019-07-13 15:32:30",
			"deleted_at": null
		}
	],
	"count": 1
}
```

## 获取商户下可显示Tab接口
* 请求接口`/auth/tabLists`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|清洗员ID|
|page|int|否|页码|
|pageSize|int|否|页面大小|

返回值
```
{
	"data": [
		{
			"id": 8,
			"title": "清洗",
			"price": "12.00",
			"is_show": 1,
			"owner_id": 1,
			"order_id": null,
			"created_at": "2019-07-13 15:32:30",
			"updated_at": "2019-07-13 15:32:30",
			"deleted_at": null
		}
	],
	"count": 1
}
```

## 添加标签Tab的接口
* 请求接口`/auth/addTab`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|客服ID|
|price|decimal(10,2)|是|价格|
|title|string|是|标题|

返回值
```
{
	"message": "添加成功",
	"status": 200
}
```

## 编辑Tab标签接口
* 请求接口`/auth/editTab`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|Tab ID|
|price|decimal(10,2)|是|价格|
|title|string|是|标题|

返回值
```
{
	"message": "编辑成功",
	"status": 200
}
```

## 显示隐藏Tab标签
* 请求接口`/auth/isShowTab`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|Tab ID|
|is_show|int|是|显示:1或者隐藏：0|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

## 给订单添加处理方案
* 请求接口`/auth/scheme`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|订单ID|
|tab_ids|string|是|添加的标签id拼接的字符串|
|scheme|string|是|添加的内容|
|price|decimal(10,2)|是|总价|
|user_id|int|是|寄售商id|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

## 不可修复接口
* 请求接口`/auth/noFix`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|订单ID|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

# 后台接口文档

## 后台登陆接口
* 请求接口`/admin/login`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|mobile|string:11|是|商户手机号|
|password|string|是|商户登陆密码|

返回值
```
{
	"access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczovL3Rlc3QudG9zbmVha2VyLmNvbS9hcGkvYWRtaW4vbG9naW4iLCJpYXQiOjE1NjMxNzIwMjQsImV4cCI6MTU2MzE3NTYyNCwibmJmIjoxNTYzMTcyMDI0LCJqdGkiOiI5M2ZpcW53QzJNMmtTckc3Iiwic3ViIjoxLCJwcnYiOiJhNTg0M2IxNzYxYzBlODJmOWNkODU5Nzc3M2FlMzE2MThjZThkZmZmIiwicm9sZSI6ImFkbWluIn0.hjLiBxGhkk89mftZdAfuCElq_QiC8_sE98IAWwTcqoE",
	"token_type": "bearer",
	"expires_in": 3600
}
```

## 后台获取用户信息接口
* 请求接口`/admin/me`
* 请求方式：默认

返回值
```
{
	"id": 1,
	"username": "测试账号",
	"password": "$2y$10$E7KXQaT2VhNPN01OIyMqe.mhc6IQRzNQjwn6bUwad1vNBP6eKee9K",
	"shop": "测试店铺",
	"mobile": "13110092730",
	"remember_token": null,
	"created_at": "2019-07-09 11:11:36",
	"updated_at": null,
	"deleted_at": null
}
```

`需要修改`
## 后台添加用户接口
* 请求接口`/admin/user`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|mobile|string:11|是|商户手机号|
|password|string min:6max:16|是|商户登陆密码|
|type|int|是|用户类型|
|username|string|是|用户名|
|owner_id|int|是|商户id|

返回值
```
{
	"message": "添加成功",
	"status": 200
}
```

`需要修改`
## 后台查询用户列表接口
* 请求接口`/admin/user`
* 请求方式：GET

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|type|int|是|用户类型|
|owner_id|int|是|商户id|
|search|string|否|查询内容|
|page|int|否|请求页码|
|num|int|否|页面大小|

返回值
```
{
	"count": 2,
	"data": [
		{
			"id": 25,
			"username": "辅导费",
			"password": "$2y$10$/wEUG9sv7cgYMYp.eH2CcOdB5HfVqSLnoe/kPS1T62vXOpfLB6Xxq",
			"type": 2,
			"mobile": "15733036829",
			"quota": "30.00",
			"owner_id": 1,
			"remember_token": null,
			"created_at": "2019-07-13 15:25:13",
			"updated_at": "2019-07-13 15:25:13",
			"deleted_at": null
		},
		{
			"id": 29,
			"username": "测试寄售商",
			"password": "$2y$10$ZnhNb2XW8QjlL/TFysSAremoNtFpaFtbx5SYU/UGtwCuh1W5ylEvu",
			"type": 2,
			"mobile": "18603532471",
			"quota": "10.00",
			"owner_id": 1,
			"remember_token": null,
			"created_at": "2019-07-15 07:47:01",
			"updated_at": "2019-07-15 07:47:01",
			"deleted_at": null
		}
	]
}
```

## 后台修改用户信息接口
* 请求接口`/admin/user`
* 请求方式：PUT

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|mobile|string:11|是|商户手机号|
|password|string min:6max:16|是|商户登陆密码|
|type|int|是|用户类型|
|username|string|是|用户名|
|id|int|是|用户id|

返回值
```
{
	"message": "success",
	"status": 200
}
```

## 后台用户订单显示列表
* 请求接口`/admin/shopList`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|商户id|
|page|int|否|当前页码|
|pageSize|int|否|页面大小|
|search|string|否|搜索内容|

返回值
```
{
	"0": {
		"id": 25,
		"username": "辅导费",
		"s1": 0,
		"s2": 0,
		"s56": 0,
		"s3": 1,
		"s7": 1,
		"s8": 1
	},
	"count": 2
}
```

## 后台用户订单显示列表
* 请求接口`/admin/orderLists`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|商户id|
|state|int|是|状态号|
|page|int|否|当前页码|
|pageSize|int|否|页面大小|

返回值
```
{
	"0": {
		"id": 25,
		"username": "辅导费",
		"s1": 0,
		"s2": 0,
		"s56": 0,
		"s3": 1,
		"s7": 1,
		"s8": 1
	},
	"count": 2
}
```

## 后台结算接口
* 请求接口`/admin/payFor`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|ids|array|是|订单id|
|pay_price|decimal(10,2)|是|支付金额|
|pay_no|string|是|支付流水号|
|shop_id|int|是|商铺ID|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

## 后台退回接口
* 请求接口`/admin/back`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|ids|array|是|订单id|
|express_compant|string|是|快递公司|
|express_code|string|是|快递单号|
|shop_id|int|是|商铺ID|

返回值
```
{
	"message": "操作成功",
	"status": 200
}
```

## 后台退回接口
* 请求接口`/admin/waitBack`
* 请求方式：默认

|请求参数|字段类型|是否必填|字段描述|
|-------|------|-------|-------|
|id|int|是|商户id|
|state|int|是|状态值5|
|page|int|否|请求页码|
|pageSize|int|否|页面大小|

返回值
```
{
	"0": {
		"id": 37,
		"consignor_id": 29,
		"bar_id": "1111111",
		"original_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/c84db7fd872c1d4.jpg\"]",
		"end_image": "[\"https:\\/\\/static.tosneaker.com\\/uploads\\/wash\\/3d0a5536fd80ad7.jpg\"]",
		"states": 5,
		"price": "11231.00",
		"tab_ids": ",9,15,",
		"scheme": "补色 ￥120.00*1 测试 ￥11111.00*1",
		"compant": null,
		"code": null,
		"created_at": "2019-07-15 15:10:13",
		"updated_at": "2019-07-15 08:18:45",
		"deleted_at": null,
		"wash_id": 30
	},
	"count": 2
}
```

