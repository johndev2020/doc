# VPN平台接口文档

[TOC]




# 0、验证码模块

## 0.0 获取图片验证码
> 获取图片验证码

HTTP请求方式
> GET {API_URL}/api/common/image/captcha


响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "token": "bfe9064a-85c3-4b6a-b5b5-7f9f9fa06e08",
    "image": "data:image/png;base64,/9j/4AAQSkZJRgABAgAAAQABAAD/....."
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|token|String|是|图片Token|
|image|String|是|图片Base64格式|



## 0.1 获取短信验证码

> 获取短信验证码

HTTP请求方式
> POST {API_URL}/api/common/v2/sms/captcha

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|version|String|是|APP当前版本号|
|phone|String|是|手机号码|
|imageToken|String|是|图片Token|
|imageCode|String|是|图片验证码|

请求参数示例（application/json）

```
{
  "appId": 0,
  "version": "4.2.6",
  "phone": "17666128230",
  "imageCode": "xknv",
  "imageToken": "bfe9064a-85c3-4b6a-b5b5-7f9f9fa06e08"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功"
}
```



## 0.2 获取邮件验证码

> 获取邮件验证码

HTTP请求方式

> POST {API_URL}/api/common/email/captcha

请求参数说明

| 参数名     | 参数类型 | 是否必需 | 描述            |
| :--------- | :------- | :------- | :-------------- |
| appId      | long     | 是       | APPID(原渠道号) |
| version    | String   | 是       | APP当前版本号   |
| email      | String   | 是       | 邮箱            |
| imageToken | String   | 是       | 图片Token       |
| imageCode  | String   | 是       | 图片验证码      |

请求参数示例（application/json）

```
{
  "appId": 0,
  "version": "4.2.6",
  "email": "123456@qq.com",
  "imageCode": "xknv",
  "imageToken": "bfe9064a-85c3-4b6a-b5b5-7f9f9fa06e08"
}
```

响应结果示例

```
{
  "code": 0,
  "message": "执行成功"
}
```



# 1、用户模块

## 1.1 手机号注册/登录
> 用户使用手机号注册/登录

HTTP请求方式
> POST {API_URL}/api/app/phone/login

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|version|String|是|APP当前版本号|
|deviceId|String|是|设备ID|
|phone|String|是|手机号码|
|captcha|String|是|短信验证码|
|channelId|long|否|推广渠道ID|
|inviterCode|String|否|邀请码|
|ticket|String|是|用户验证票据|
|randStr|String|是|随机字符串|
|userIp|String|是|用户外网IP|

请求参数示例（application/json）
```
{
  "appId": 0,
  "version": "4.2.6",
  "captcha": "265963",
  "channelId": 0,
  "deviceId": "string",
  "inviterCode": "string",
  "phone": "string",
  "ticket": "string",
  "randStr": "string",
  "userIp": "string"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "userId": "267687876139941888",
    "accessToken": "3f6850c32b5b4da4996c636d727bb0c2",
    "isNewUser": true,
    "messages": [
      {
        "title": "新人礼包",
        "message": "恭喜您获得 3天体验套餐。您也可以邀请好友注册获得更多免费套餐。"
      }
    ],
    "userProfile": {
        "username": "",
        "phone": "18812345678",
        "email": "123456@qq.com",
        "promotionChannelId": "0",
        "secretKey": "bc1023ff-36ee-432f-a9e9-aca89ae13d0b",
        "expired": false,
        "paying": true,
        "expireTime": "2020-12-03 11:10:31",
        "loginTime": "2020-04-27 10:01:24",
        "createTime": "2020-05-13 10:00:12",
        "signedToday": false,
        "signedDays": 3,
        "signedDuration": 60,
        "signInfo": {
          "signedToday": false,
          "signedDays": 3,
          "signedAward": "测试1111"
        },
        "packagesBalance": {
          "usedDataTraffic": 0,
          "totalDataTraffic": 1536
        },
        "userId": "219134863448023102"
      },
    "defaultNode": {
      "name": "孟买ssr",
      "nameEn": "India",
      "platform": "linode",
      "areaCode": "IN",
      "areaName": "印度",
      "serverIp": "172.105.60.39",
      "serverPort": 41285,
      "protocol": 8,
      "maxDataTraffic": 0,
      "usedDataTraffic": 0,
      "maxTerminalNumber": 500,
      "usedTerminalNumber": 179,
      "description": "",
      "nodeId": "03046d28777148c2a56cc07ac295f29f"
    }
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|userId|long|是|用户ID|
|isNewUser|boolean|是|是否为新用户(true:是，false:否)|
|accessToken|String|是|访问票据|
|messages|Array|否|获赠套餐信息|
|userProfile|Object|是|详见1.5接口|



## 1.2 邮箱注册

> 用户使用邮箱注册

HTTP请求方式
> POST {API_URL}/api/app/email/register

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|version|String|是|APP当前版本号|
|deviceId|String|是|设备ID|
|email|String|是|邮箱|
|password|String|是|密码|
|channelId|long|否|推广渠道ID|
|inviterCode|String|否|邀请码|
|ticket|String|是|用户验证票据|
|randStr|String|是|随机字符串|
|userIp|String|是|用户外网IP|

请求参数示例（application/json）
```
{
  "appId": 0,
  "version": "4.2.6",
  "channelId": 0,
  "deviceId": "string",
  "email": "string",
  "inviterCode": "string",
  "password": "string",
  "ticket": "string",
  "randStr": "string",
  "userIp": "string"
}
```

响应结果示例
同 1.1

响应结果说明
同 1.1

## 1.3 邮箱登录

> 用户使用邮箱登录

HTTP请求方式
> POST {API_URL}/api/app/email/login

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|version|String|是|APP当前版本号|
|deviceId|String|是|设备ID|
|email|String|是|邮箱|
|password|String|是|密码|
|channelId|long|否|推广渠道ID|
|inviterCode|String|否|邀请码|


请求参数示例（application/json）
```
{
  "appId": 0,
  "version": "4.2.6",
  "channelId": 0,
  "deviceId": "string",
  "email": "string",
  "inviterCode": "string",
  "password": "string"
}
```

响应结果示例
同 1.1

响应结果说明
同 1.1


## 1.4 匿名登录

> 用户使用设备ID匿名登录

HTTP请求方式
> POST {API_URL}/api/app/anonymous/login

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|version|String|是|APP当前版本号|
|deviceId|String|是|设备ID|
|channelId|long|否|推广渠道ID|
|inviterCode|String|否|邀请码|
|ticket|String|是|用户验证票据|
|randStr|String|是|随机字符串|
|userIp|String|是|用户外网IP|

请求参数示例（application/json）
```
{
  "appId": 0,
  "version": "4.2.6",
  "channelId": 0,
  "deviceId": "string",
  "inviterCode": "string",
  "ticket": "string",
  "randStr": "string",
  "userIp": "string"
}
```

响应结果示例
同 1.1

响应结果说明
同 1.1



## 1.5 用户资料

> 用户个人资料

HTTP请求方式
> POST {API_URL}/api/app/auth/user/profile

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "username": "",
    "phone": "18812345678",
    "email": "123456@qq.com",
    "promotionChannelId": "0",
    "secretKey": "bc1023ff-36ee-432f-a9e9-aca89ae13d0b",
    "expired": false,
    "paying": true,
    "expireTime": "2020-12-03 11:10:31",
    "loginTime": "2020-04-27 10:01:24",
    "createTime": "2020-05-13 10:00:12",
    "signedToday": false,
    "signedDays": 3,
    "signedDuration": 60,
    "signInfo": {
      "signedToday": false,
      "signedDays": 3,
      "signedAward": "测试1111"
    },
    "packagesBalance": {
      "usedDataTraffic": 0,
      "totalDataTraffic": 1536
    },
    "userId": "219134863448023102"
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|userId|long|是|用户ID|
|phone|String|是|手机号|
|email|String|是|邮箱|
|promotionChannelId|long|是|推广渠道ID|
|secretKey|String|是|用户秘钥|
|expired|boolean|是|套餐是否过期（是：true，否：false）|
|paying|boolean|是|是否为付费用户（是：true，否：false）|
|expireTime|String|是|套餐过期时间|
|loginTime|String|是|最后登录时间|
|createTime|String|是|注册时间|
|~~signedToday~~|~~boolean~~|~~是~~|~~今日是否签到（是：true，否：false）~~|
|~~signedDays~~|~~int~~|~~是~~|~~累计签到天数~~|
|~~signedDuration~~|~~int~~|~~是~~|~~每日签到可获得时长（分钟）~~|
|signInfo|Object|是|签到信息|
|signedToday|boolean|是|今日是否签到（是：true，否：false）|
|signedDays|int|是|累计签到天数|
|signedAward|String|是|每日签到可获得套餐名称|
|packagesBalance|Object|否|套餐余额|
|totalDataTraffic|decimal(10,2)|是|套餐包含流量（MB）,0 表示不限制|
|usedDataTraffic|decimal(10,2)|是|已用流量（MB）|



## 1.6 用户签到

> 用户签到

HTTP请求方式
> POST {API_URL}/api/app/auth/user/sign

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

响应结果示例
```
{
  "code": 0,
  "message": "签到成功,已获得15分钟套餐 "
}
```



## 1.7 绑定手机号

> 用户绑定手机号

HTTP请求方式
> POST {API_URL}/api/app/auth/user/bind/phone

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|phone|String|是|手机号|
|captcha|String|是|短信验证码|

请求参数示例（application/json）
```
{
  "captcha": "string",
  "phone": "string"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "操作成功"
}
```



## 1.8 绑定邮箱

> 用户绑定邮箱

HTTP请求方式
> POST {API_URL}/api/app/auth/user/bind/email

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|email|String|是|邮箱|
|password|String|是|新密码|

请求参数示例（application/json）
```
{
  "email": "string",
  "password": "string"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "操作成功"
}
```



## 1.9 修改密码

> 用户修改密码

HTTP请求方式
> POST {API_URL}/api/app/auth/user/update/password

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|email|String|是|邮箱|
|passwordOld|String|是|原密码|
|password|String|是|新密码|

请求参数示例（application/json）
```
{
  "email": "string",
  "passwordOld": "string",
  "password": "string"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "操作成功"
}
```



## 1.10 防丢失页面

> 用户防丢失页面

HTTP请求方式
> POST {API_URL}/api/app/auth/user/loss

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "userId": "318066754112716800",
    "show": true,
    "mandatory": false,
    "description": "防丢失页面描述",
    "qrcodeContent": "http://www.baidu.com?userId=318066754112716800&appId=1000"
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|userId|long|是|用户ID|
|show|boolean|是|是否显示（是：true，否：false）|
|mandatory|boolean|是|是否强制绑定（是：true，否：false）|
|description|String|是|防丢失页面描述|
|qrcodeContent|String|是|二维码内容|



## 1.11 扫码登录

> 用户扫码登录

HTTP请求方式
> POST {API_URL}/api/app/qrcode/scan

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|ticket|String|是|二维码中的登录票据|

请求参数示例（application/json）
```
{
  "ticket": "string"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功"
}
```



## 1.12 扫码后确认

> 用户扫码后确认登录

HTTP请求方式
> POST {API_URL}/api/app/auth/qrcode/confirm

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|ticket|String|是|二维码中的登录票据|

请求参数示例（application/json）
```
{
  "ticket": "string"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功"
}
```



## 1.13 通过邮箱找回密码

> 通过邮箱找回密码

HTTP请求方式

> POST {API_URL}/api/app/user/find/password

请求参数说明

| 参数名   | 参数类型 | 是否必需 | 描述            |
| :------- | :------- | :------- | :-------------- |
| appId    | long     | 是       | APPID(原渠道号) |
| version  | String   | 是       | APP当前版本号   |
| email    | String   | 是       | 邮箱            |
| captcha  | String   | 是       | 邮件验证码      |
| password | String   | 是       | 新密码          |

请求参数示例（application/json）

```
{
  "appId": 1000,
  "version": "4.3.0.1",
  "email": "123456@qq.com"
  "captcha": "265963",
  "password": "123456"
}
```

响应结果示例

```
{
  "code": 0,
  "message": "操作成功"
}
```



# 2、套餐模块

## 2.1 套餐列表
> 查询系统套餐列表

HTTP请求方式
> POST {API_URL}/api/app/auth/package/list

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|version|string|否|APP版本号|

请求参数示例（application/json）
```
{
  "version": "2.0.1"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": [
    {
      "packageId": "1",
      "chargeType": "1",
      "duration": 30,
      "province": "广东",
      "originalPrice": 50,
      "price": 30,
      "dataTraffic": 102400,
      "terminalNumber": 5,
      "description": "",
      "packageName": "100G/30天套餐",
      "endTime":"2020-10-01 00:00:00"
    }
  ]
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|packageId|long|是|套餐ID|
|chargeType|int|是|计费类型(1:按时长,2:按流量)|
|packageName|String|是|套餐名称|
|packageNameEn|String|是|套餐名称(en)|
|province|String|是|归属地|
|duration|int|是|时长(天)|
|originalPrice|decimal(10,2)|是|原价格(元)|
|price|decimal(10,2)|是|现价格(元)|
|dataTraffic|decimal(10,2)|是|包含的流量（MB），0表示不限制|
|terminalNumber|int|是|允许的终端数，0表示不限制|
|endTime|String|否|限时优惠套餐订购截止时间(yyyy-MM-dd HH:mm:ss)|



## 2.2 套餐详情

> 查询套餐详情

HTTP请求方式
> POST {API_URL}/api/app/auth/package/info

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|packageId|long|是|套餐ID|

请求参数示例（application/json）
```
{
  "packageId": 105629843021
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
  	"packageId": "1",
    "chargeType": "1",
    "duration": 30,
    "province": "广东",
    "originalPrice": 50,
    "price": 30,
    "dataTraffic": 102400,
    "terminalNumber": 5,
    "description": "100G/30天套餐",
    "packageName": "100G/30天套餐",
    "endTime":""
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|packageId|long|是|套餐ID|
|chargeType|int|是|计费类型(1:按时长,2:按流量)|
|packageName|String|是|套餐名称|
|packageNameEn|String|是|套餐名称(en)|
|province|String|是|归属地|
|duration|int|是|时长(天)|
|originalPrice|decimal(10,2)|是|原价格(元)|
|price|decimal(10,2)|是|现价格(元)|
|dataTraffic|decimal(10,2)|是|包含的流量（MB），0表示不限制|
|terminalNumber|int|是|允许的终端数，0表示不限制|
|description|String|是|套餐的介绍|
|descriptionEn|String|是|套餐的介绍|
|endTime|String|否|限时优惠套餐订购截止时间(yyyy-MM-dd HH:mm:ss)|



## 2.3 我订购的套餐

> 查询我订购的套餐

HTTP请求方式

> POST {API_URL}/api/app/auth/user/package/list

请求头说明

| 参数名      | 参数类型 | 是否必需 | 描述     |
| : | :------- | :------- | :------- |
| AccessToken | Header   | 是       | 访问票据 |

响应结果示例

```
{
  "code": 0,
  "message": "执行成功",
  "data": [
    {
      "packageName": "套餐2",
      "beginTime": "2019-08-01 10:20:00",
      "endTime": "2019-09-30 10:20:02",
      "dataTraffic": 0,
      "packageDataTraffic": 102400,
      "usedDataTraffic": 10,
      "packageTerminalNumber": 5,
      "usedTerminalNumber": "2"
    }
  ]
}
```

响应结果说明

| 参数名                | 参数类型      | 是否必需 | 描述                            |
| : | :-- | :------- | : |
| userPackageId         | long          | 是       | 用户套餐ID                      |
| packageName           | String        | 是       | 套餐名称                        |
| packageNameEn         | String        | 是       | 套餐名称                        |
| beginTime             | String        | 是       | 开始时间                        |
| endTime               | String        | 是       | 截止时间                        |
| usedDataTraffic       | decimal(10,2) | 是       | 已使用流量（MB）                |
| packageDataTraffic    | decimal(10,2) | 是       | 套餐内总流量（MB），0表示不限制 |
| usedTerminalNumber    | int           | 是       | 已使用终端数                    |
| packageTerminalNumber | int           | 是       | 套餐内总终端数，0表示不限制     |



## 2.4 首单优惠弹窗

> 首单优惠弹窗

HTTP请求方式

> POST {API_URL}/api/app/auth/first/discount/info

请求头说明

| 参数名      | 参数类型 | 是否必需 | 描述     |
| :---------- | :------- | :------- | :------- |
| AccessToken | Header   | 是       | 访问票据 |

请求参数说明

| 参数名  | 参数类型 | 是否必需 | 描述      |
| :------ | :------- | :------- | :-------- |
| version | string   | 否       | APP版本号 |

请求参数示例（application/json）

```
{
  "version": "4.3.0.1"
}
```

响应结果示例

```
{
  "code": 0,
  "message": "执行成功",
  "data": {
      "content": "购买30天套餐，赠送10天\n购买30天套餐，赠送10天",
      "endTime":"2020-10-01 00:00:00"
    }
}
```

响应结果说明

| 参数名        | 参数类型      | 是否必需 | 描述                                      |
| :------------ | :------------ | :------- | :---------------------------------------- |          |
| content       | String        | 是       | 优惠信息                                  |
| endTime       | String        | 是       | 优惠套餐订购截止时间(yyyy-MM-dd HH:mm:ss) |



# 3、节点模块


## 3.1 节点列表
> 查询套餐内节点列表

HTTP请求方式
> POST {API_URL}/api/app/auth/node/list

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": [
    {
      "name": "节点21",
      "platform": "AWS",
      "areaCode": "KR",
      "areaName": "韩国",
      "serverIp": "11.22.33.44",
      "serverPort": 41285,
      "protocol": 1,
      "maxDataTraffic": 100,
      "usedDataTraffic": 10,
      "maxTerminalNumber": 10,
      "usedTerminalNumber": 2,
      "description": "",
      "nodeId": "21"
    },
    {
      "name": "节点22",
      "platform": "AWS",
      "areaCode": "JP",
      "areaName": "日本",
      "serverIp": "11.22.33.44",
      "serverPort": 41285,
      "protocol": 1,
      "maxDataTraffic": 100,
      "usedDataTraffic": 100,
      "maxTerminalNumber": 10,
      "usedTerminalNumber": 10,
      "description": "",
      "nodeId": "22"
    }
  ]
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|nodeId|String|是|节点ID|
|name|String|是|节点名称|
|nameEn|String|是|节点名称(en)|
|platform|String|是|节点所属平台|
|areaCode|String|是|节点地区代码|
|areaName|String|是|节点地区名称|
|serverIp|String|是|节点IP地址|
|serverPort|int|是|节点端口|
|protocol|int|是|协议类型2^n (1:L2TP,2:IKEv2,4:IPsec,8:SHADOWSOCKS,16:https,32:vmess,64:Trojan)|
|maxDataTraffic|decimal(10,2)|是|最大流量|
|usedDataTraffic|decimal(10,2)|是|已使用流量|
|maxTerminalNumber|int|是|最大终端数|
|usedTerminalNumber|int|是|已连接终端数|
|description|String|是|节点描述|
|authType|String|是|鉴权类型(1:节点秘钥,2:用户秘钥)|
|ext1|String|是|扩展参数1|
|ext2|String|是|扩展参数2|
|ext3|String|是|扩展参数3|
|ext4|String|是|扩展参数4|
|ext5|String|是|扩展参数5|
|ext6|String|是|扩展参数6|



# 4、版本 / 配置

## 4.1 获取APP最新版本
> 获取最新APP版本

HTTP请求方式
> POST {API_URL}/api/app/version/latest

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|os|int|是|系统类型(1:Android，2:iOS)|
|version|String|否|APP当前版本号|

请求参数示例（application/json）
```
{
  "os": 1,
  "appId": 1000
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "os": 1,
    "version": "1.0.0",
    "mandatory": false,
    "url": "https://www.baidu.com",
    "updateTime": "2018-09-20",
    "description": "更新内容描述"
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|os|int|是|系统类型(1:Android,2:iOS,3:Windows,4:Mac)|
|version|String|是|目标版本号|
|mandatory|boolean|是|是否强制更新(true:是，false:否)|
|url|String|是|下载地址|
|updateTime|String|是|更新时间|
|description|String|是|更新内容描述|
|descriptionEn|String|是|更新内容描述|



## 4.2 获取APP配置信息

> 获取APP配置信息

HTTP请求方式
> POST {API_URL}/api/app/configs

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|group|String|否|配置分组|
|key|String|否|配置键|
|version|String|否|版本|

请求参数示例（application/json）
```
{
  "group": "",
  "key": "ios_pswlogin_enable",
  "version": "1.0.1",
  "appId": 1000
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": [
    {
      "key": "ios_pswlogin_enable",
      "value": "1",
      "version": "1.0.1",
      "desc": "是否开启密码登录"
    }
  ]
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|key|String|是|配置键|
|value|boolean|是|配置值|
|desc|String|是|配置描述|



# 5、订单模块

## 5.1 订单列表
> 查询我的订单列表

HTTP请求方式
> POST {API_URL}/api/app/auth/order/list


请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": [
    {
      "packageId": "1001",
      "packageName": "100G/30天套餐",
      "orderFee": 30,
      "payFee": 0,
      "payStatus": 2,
      "payTime": "",
      "payUrl": "",
      "createTime": "2019-09-06 18:15:21",
      "orderId": "222419428480909312"
    },
    {
      "packageId": "1001",
      "packageName": "100G/30天套餐",
      "orderFee": 30,
      "payFee": 0,
      "payStatus": 0,
      "payTime": "",
      "payUrl": "https//xxxxxxxx",
      "createTime": "2019-09-06 11:27:59",
      "orderId": "222316908567855104"
    }
  ]
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|
|packageId|long|是|套餐ID|
|packageName|String|是|套餐名称|
|packageNameEn|String|是|套餐名称|
|payStatus|String|是|支付状态(0:未支付,1:支付成功,2:支付失败)|
|orderFee|decimal(10,2)|是|订单金额(元)|
|payFee|decimal(10,2)|是|支付金额(元)|
|payTime|String|否|支付时间|
|payUrl|String|否|支付地址|
|createTime|String|是|订单时间|



## 5.2 订单详情

> 查询订单详情

HTTP请求方式
> POST {API_URL}/api/app/auth/order/info

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|

请求参数示例（application/json）
```
{
  "orderId": 222419428480909312
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "packageId": "1001",
    "packageName": "100G/30天套餐",
    "orderFee": 1,
    "payFee": 0,
    "payStatus": 0,
    "payTime": "",
    "payUrl": "https//xxxxxxxx",
    "description": ""
    "createTime": "2019-09-06 18:15:21",
    "orderId": "222419428480909312"
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|
|packageId|long|是|套餐ID|
|packageName|String|是|套餐名称|
|packageNameEn|String|是|套餐名称|
|payStatus|String|是|支付状态(0:未支付,1:支付成功,2:支付失败)|
|orderFee|decimal(10,2)|是|订单金额(元)|
|payFee|decimal(10,2)|是|支付金额(元)|
|payTime|String|否|支付时间|
|payUrl|String|否|支付地址|
|description|String|是|订购描述信息|
|createTime|String|是|订单时间|



## 5.3 提交订单

> 提交订单

HTTP请求方式
> POST {API_URL}/api/app/auth/order/create

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|packageId|long|是|套餐ID|
|quantity|int|是|购买数量(终端数)|
|os|int|是|系统类型(1:Android,2:iOS,3:Windows,4:Mac)|
|version|String|是|APP版本|


请求参数示例（application/json）
```
{
  "packageId": 1001,
  "quantity": 3,
  "os": 1,
  "version": "4.2.2"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "orderId": "297418533011193856",
    "packageId": "1001",
    "orderFee": 30,
    "packageName": "30天套餐",
    "packageNameEn": "",
    "description": "",
    "payTypes": [
      {
        "payTypeId": "1",
        "payType": "ali_wap",
        "payTypeName": "支付宝H5"
      },
      {
        "payTypeId": "3",
        "payType": "ali_qrcode",
        "payTypeName": "支付宝扫码"
      },
      {
        "payTypeId": "4",
        "payType": "google_app",
        "payTypeName": "谷歌应用内支付"
      }
    ]
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|
|packageId|long|是|套餐ID|
|packageName|String|是|套餐名称|
|packageNameEn|String|是|套餐名称|
|orderFee|decimal(10,2)|是|订单金额(元)|
|description|String|是|订购描述信息|
|payTypes|array|是|支付方式列表|
|payTypeId|int|是|支付方式ID|
|payType|String|是|支付方式|
|payTypeName|String|是|支付方式名称|



## 5.4 订单支付
> 订单支付

HTTP请求方式
> POST {API_URL}/api/app/auth/order/topay

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|
|payTypeId|int|是|支付方式ID|

请求参数示例（application/json）
```
{
  "orderId": 297418533011193856,
  "payTypeId": 1
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "orderId": "297418533011193856",
    "payOrderId": "297418533011190000",
    "packageId": "1001",
    "orderFee": 1,
    "packageName": "30天套餐",
    "packageNameEn": "",
    "payTypeId": "1",
    "payType": "ali_wap",
    "payTypeName": "支付宝H5",
    "payUrl": "https://render.alipay.com/p/s/i?scheme=alipays%3a%2f%2fplatformapi%2fstartApp%3fappId%3d20000125%26orderSuffix%3dh5_route_token%253d%2522RZ24phLXrs9maDXCnvolzo1be0VVHDmobilecashierRZ24%2522%2526is_h5_route%253d%2522true%2522",
    "description": ""
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|
|payOrderId|long|是|交易订单号|
|packageId|long|是|套餐ID|
|packageName|String|是|套餐名称|
|packageNameEn|String|是|套餐名称|
|orderFee|decimal(10,2)|是|订单金额(元)|
|description|String|是|订购描述信息|
|payUrl|String|是|支付地址|
|payTypeId|int|是|支付方式ID|
|payType|String|是|支付方式|
|payTypeName|String|是|支付方式名称|



## 5.5 支付方式列表
> 获取当前支持的支付方式列表

HTTP请求方式
> POST {API_URL}/api/app/auth/paytype/list

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|os|int|是|系统类型(1:Android,2:iOS,3:Windows,4:Mac)|
|version|String|是|APP版本|


请求参数示例（application/json）
```
{
  "os": 1,
  "version": "4.2.2"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": [
      {
        "payTypeId": "1",
        "payType": "ali_wap",
        "payTypeName": "支付宝H5"
      },
      {
        "payTypeId": "3",
        "payType": "ali_qrcode",
        "payTypeName": "支付宝扫码"
      },
      {
        "payTypeId": "4",
        "payType": "google_app",
        "payTypeName": "谷歌应用内支付"
      }
   ]
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|payTypeId|int|是|支付方式ID|
|payType|String|是|支付方式|
|payTypeName|String|是|支付方式名称|



## 5.6 苹果IAP订单校验

> 苹果IAP订单校验

HTTP请求方式

> POST {API_URL}/api/app/auth/iap/receipt

请求头说明

| 参数名      | 参数类型 | 是否必需 | 描述     |
| : | :------- | :------- | :------- |
| AccessToken | Header   | 是       | 访问票据 |

请求参数说明

| 参数名      | 参数类型 | 是否必需 | 描述                         |
| : | :------- | :------- | :------- |
| orderId     | long     | 是       | 订单ID                       |
| receiptData | String   | 是       | 回执信息字符串（Base64编码） |

请求参数示例（application/json）

```
{
  "orderId": 222419428480909312,
  "receiptData": "JTdCJTBBJTIwJTIwJTIwJTIwJTIycmVjZWlwdCUQSUyMCUyMCUyMCUyMCUyMnN0YXR1cyUyMiUzQSUyMDAlMEElN0Q="
}
```

响应结果示例

```
{
  "code": 0,
  "message": "执行成功"
}
```



## 5.7 谷歌IAP订单校验

> 谷歌IAP订单校验

HTTP请求方式

> POST {API_URL}/api/app/auth/google/iap/receipt

请求头说明

| 参数名      | 参数类型 | 是否必需 | 描述     |
| : | :------- | :------- | :------- |
| AccessToken | Header   | 是       | 访问票据 |

请求参数说明

| 参数名     | 参数类型 | 是否必需 | 描述           |
| :--------- | :------- | :------- | :--- |
| signedData | String   | 是       | 谷歌签名源报文 |
| signature  | String   | 是       | 谷歌签名结果   |

请求参数示例（application/json）

```
{
  "signedData": "{\"orderId\":\"GPA.3347-0000-0966-74443\",\"packageName\":\"com.feeker.vpn\",\"productId\":\"1234567890\",\"purchaseTime\":1581931731155,\"purchaseState\":0,\"developerPayload\":\"inapp:1234567890:f9903c6e-9d26-4535-a3cf-daf30c3cfa94:1111111111112\",\"purchaseToken\":\"baaliajjlbhodplcidghghef.AO-J1Oxnyr4EMYoNdQFekMqgDh3if-NLLmEOGH8uEhVBGlb4jP40GEJOMGm2BRxsaKsRbut19Ebnxiw-YV4YvnH0lNKCrXPAloX3trQy1JEStTD1RjDE5ok\"}",
  "signature": "akPUiDDeBAJ/e3i1Fr4EJk3VUZDf6XZOLFx2ynHGQCeNHcMo8kEhDLncmcXS4rARwN5OfB7+3hs/jA3er9qKv4FKrudqWD7MDcsCnJHZL8IKonnZ+0xurCEDXZyhZj251SDe8EzcknrXQ5eXtaGYFMd0Seug9OWim75faADhA/Ss8m+4wVhuYf5IoL+/QPAHWzJL8bnn0lFH+6C4yOgPcKH9U/QffG/6aRN0i8hZbxl8e8OkugDWMC2judWuhL82Y7kptKoznZyXVALIaiLFHuTeQmuKbzctCQ3eT20bGPPvA1bPkVJ/iejPeZtSK7Q9zX+j5XzLxIWjmeiI7uBRdw=="
}
```

响应结果示例

```
{
  "code": 0,
  "message": "执行成功"
}
```



## 5.8 查询订单支付结果

> 查询订单支付结果

HTTP请求方式
> POST {API_URL}/api/app/auth/order/pay/result

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|
|payOrderId|long|是|交易订单号|


请求参数示例（application/json）
```
{
  "orderId": 1001,
  "payOrderId": 2001
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "orderId": 1001,
    "payOrderId": 2001,
    "success": false
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|orderId|long|是|订单ID|
|payOrderId|long|是|交易订单号|
|success|boolean|是|是否支付（是：true，否：false）|



# 6、公告模块

## 6.1 获取未读公告数量
> 获取未读公告数量

HTTP请求方式
> POST {API_URL}/api/app/auth/notice/unread

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|latestTime|String|是|本地最近更新时间（yyyy-MM-dd HH:mm:ss）|
|os|int|是|系统类型(1:Android,2:iOS,3:Windows,4:Mac)|
|version|String|是|APP版本|

请求参数示例（application/json）
```
{
  "latestTime": "2019-01-01 00:00:00",
  "os": 1,
  "version": "4.1.0.1"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "latestTime": "2019-12-01 00:00:00",
    "count": 5
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|latestTime|String|是|最新公告时间（yyyy-MM-dd HH:mm:ss）|
|count|int|是|新公告数量|



## 6.2 获取最新强制公告信息

> 获取最新强制公告信息

HTTP请求方式
> POST {API_URL}/api/app/auth/notice/mandatory/list

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|os|int|是|系统类型(1:Android,2:iOS,3:Windows,4:Mac)|
|version|String|是|APP版本|

请求参数示例（application/json）
```
{
  "os": 1,
  "version": "4.1.0.1"
}
```


响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": [
    {
      "id": "1001",
      "title": "公告标题",
      "content": "公告内容",
      "showSecond": 5,
      "createTime": "2019-09-06 18:15:21"
    }
  ]
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|id|String|是|公告ID|
|title|String|是|公告标题|
|content|String|是|公告内容|
|showSecond|int|是|弹窗显示秒数|
|createTime|String|是|公告发布时间（yyyy-MM-dd HH:mm:ss）|



# 7、跑马灯模块

## 7.1 获取最新跑马灯内容
> 获取最新跑马灯内容

HTTP请求方式
> POST {API_URL}/api/app/auth/announcement

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|os|int|是|操作系统(1:Android,2:iOS,3:Windows,4:Mac)|

请求参数示例（application/json）
```
{
  "os": 1
}
```

响应结果示例
```
{
  "code": 0,
  "message": "执行成功",
  "data": {
    "id": "279295387448115200",
    "title": "AAAA",
    "content": "BBBBBBB",
    "url": "https://www.google.com",
    "updateTime": "2020-02-10 17:39:08",
    "createTime": "2020-02-10 17:00:07"
  }
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|id|long|是|跑马灯ID|
|title|String|是|标题|
|content|String|是|内容|
|url|String|否|跳转地址|
|updateTime|String|是|更新时间（yyyy-MM-dd HH:mm:ss）|
|createTime|String|是|发布时间（yyyy-MM-dd HH:mm:ss）|



# 8、消息推送模块

## 8.1 设备注册
> 用户登录后将设备信息注册到平台，每次打开APP时都需提交注册信息。

HTTP请求方式
> POST {API_URL}/api/app/auth/device/register

请求头说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|AccessToken|Header|是|访问票据|

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appkey|String|是|友盟平台应用ID|
|os|int|是|操作系统(1:Android,2:iOS)|
|deviceId|String|是|友盟设备Id|
|appVersion|String|是|一键连APP版本|

请求参数示例（application/json）
```
{
  "appkey": "5e3a94dc4ca35738780007f1",
  "appVersion": "4.1.0.2",
  "deviceId": "765286352546",
  "os": "1"
}
```
响应结果示例
```
{
  "code": 0,
  "message": "执行成功"
}
```



# 9、话单同步模块

## 9.1 同步用户话单
> 按日将用户话单数据汇总后同步到平台

HTTP请求方式
> POST {API_URL}/api/syn/user/bills

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|userId|long|是|用户ID|
|billDate|String|是|日期(yyyy-MM-dd)|
|dataTraffic|decimal|是|使用的流量(MB)，保留4位小数|
|ips|int|是|IP数量|

请求参数示例（application/json）
```
[
	{
	  "userId": 219134863448023102,
	  "billDate": "2020-04-09",
	  "dataTraffic": "89.5600",
	  "ips": 5
	},
	{
	  "userId": 222358323888914432,
	  "billDate": "2020-04-09",
	  "dataTraffic": "13543.1200",
	  "ips": 1
	}
]
```
响应结果示例
```
{
  "code": 0,
  "message": "执行成功"
}
```



# 10、广告信息

## 10.1 获取广告列表
> 获取广告列表

HTTP请求方式
> POST {API_URL}/api/app/ad/list

请求参数说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|appId|long|是|APPID(原渠道号)|
|os|int|是|系统类型(1:Android,2:iOS,3:Windows,4:Mac)|
|version|String|否|APP当前版本号|

请求参数示例（application/json）
```
{
  "os": 1,
  "appId": 1000,
  "version":"4.2.3"
}
```

响应结果示例
```
{
  "code": 0,
  "message": "string",
  "data": [
    {
      "id": 100000,
      "jumpUrl": "http://www.baidu.com",
      "material": "http://www.baidu.com/logo.png",
      "name": "广告名称",
      "space": "index_top",
      "timePeriod": "00:00~24:00",
      "enableGuest": false,
      "enablePaying": false,
    }
  ]
}
```

响应结果说明
|参数名|参数类型|是否必需|描述|
|:------|:-------|:------|:---------|
|id|long|是|广告ID|
|name|String|是|广告名称|
|space|String|是|广告位标识，详见 10.1.6|
|material|String|是|广告素材|
|jumpUrl|String|是|跳转链接|
|timePeriod|String|是|展示时间段|
|enableGuest|boolean|是|是否对游客展示(false:否,true:是)|
|enablePaying|boolean|是|是否对付费用户展示(false:否,true:是)|


广告位标识说明
|广告位标识|描述|
|:------|:-------|
|app_launch|APP启动页|
|index_top|首页顶部|
|package_top|套餐页面顶部|
|order_top|订单页面顶部|
|sign_popup|签到成功弹窗|
|recommend_top|推荐网站顶部|





# 状态码说明

|code|message|状态说明|
|:------|:-------|:------|
|0|执行成功|本次业务操作执行成功|
|204|查询结果为空|本次查询结果为空|
|300|执行失败|本次业务操作执行失败|
|301|套餐已过期|套餐已过期|
|400|请求参数错误|请检查请求参数是否正确|
|401|未授权的访问|未登录，请登录后再访问|
|402|无效的Token|Token不合法或者已过期，请重新登录|
|403|禁止访问|权限不够，请求被拒绝|
|500|系统异常|请根据异常提示信息处理|
