+ 2018年5月24日
    + API初始化

+ 2018年6月26日
    + 修改公众号结构，包括以下几点
    	+ 添加qrCode字段
    	+ 修改region字段为regionId
    	+ 修改classfy字段为categoryId
+ 2018年6月28日
    + 添加地区管理接口
    + 添加分类管理接口

## 文件上传
### 获取上传文件验证 (GET) [/upload] (本接口是support服务提供的，所以完整url为/support/upload)
+ Data
    + code (string) - 固定值
    + isPublic (int) - 固定值
    + time (long) - 时间戳
    + userId (long) - 当前用户id
    + key (string) - 验证串
+ Description
    + [MUST] Authenticated
+ Response 200 (application/json)

        {
          "data": {
            "isPublic": 1,
            "code": "20160725001",
            "time": 1527152862645,
            "userId": 1031,
            "key": "456c1c8ae1f5223527b0478219303145"
          }
        }
### 上传文件 (POST) [http://192.168.1.248/upload/image] 
+ Request (application/form-data)

        {
          "code": "20160725001",
          "isPublic": 1,
          "time": 1491885189308,
          "userId": 12,
          "key": "afb66afa0404f92ac4670f6f4a721779"
          "file": "avatar.jpg"
        }
+ Response 200 (application/json)

        {
              "code": 100,
              "message": null,
              "data": {
                  "url":"http://static.budee.com/iyyren/image/201704/11/1234/195238888195899392.jpg"
              },
              "error": null
          }

## 公众号管理
+ Data
    + articleSeedId (Long) - seed与article的seed表id对应表 
    + title (String) - 微信号名称
    + wechatId (String) - 微信号wechat_id
    + funcIntro (String) - 功能介绍
    + biz (String) - 公众号唯一识别符（唯一）
    + logo (String) - 公众号logo
    + qrCode (String) - 二维码
    + accountType (int) - 订阅号0   服务号1
    + accountSubject (int) - 企业和个人
    + companyName (String) - 企业全称
    + businessRegNo (String) - 工商执照注册号
    + serviceTel (String) - 客服电话
    + companyType (String) - 企业类型
    + businessScope (String) - 经营范围
    + establishDate (date) - 企业成立日期
    + operatingPeriod (date) - 企业经营期限
    + regionId (long) - 地区
    + categoryId (long) - 分类
    + description (String) - 描述
    + updateRate (int) - 更新频率
    + language (int) - 0中文  1英文
    + enabled (int)  - 使能  0禁止 1启用
    + creator (long) - 创建人
    + modifier (long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
    
### 增加 [POST] /wxSeeds
+ Description
    + [MUST] Authenticated
    + [MUST] ROLE_ADMIN
+ Parameters
    + articleSeedId
    + title 必填
    + wechatId 必填
    + funcIntro
    + biz
    + logo
    + qrCode
    + accountType
    + accountSubject
    + companyName
    + businessRegNo
    + serviceTel
    + companyType
    + businessScope
    + establishDate
    + operatingPeriod
    + regionId
    + categoryId
    + description
    + updateRate
    + language
+ Request（application/json）

        {
            "data":{
                "title":"未来无限可能",
                "wechatId":"feiguohai123"
            }
        }
       
+ Response 201 (application/json)  

        {
          "data": {
            "id": 74,
            "type": "wxSeeds"
          }
        }
       
### 修改 [PATCH] /wxSeeds/{id}
+ Description
    + [MUST] Authenticated
    + [MUST] ROLE_ADMIN
+ Parameters
    + articleSeedId
    + title 必填
    + wechatId 必填
    + funcIntro
    + biz
    + logo
    + qrCode
    + accountType
    + accountSubject
    + companyName
    + businessRegNo
    + serviceTel
    + companyType
    + businessScope
    + establishDate
    + operatingPeriod
    + regionId
    + categoryId
    + description
    + updateRate
    + language
       
+ 修改Request 200（application/json）

        {
            "data":{
                "title":"我的未来无限可能",
                "wechatId":"feiguohai123",
                "biz":"woshiweiyibiaoshifu"
            }
        }
+  Response 200       


### 列表 [GET] /wxSeeds?filter[title:like]=%25Midifan%25&page[number]=1&page[size]=5&sort=-modified      
       
+ Parameters
  + id 
  + title
     + 查询示例：filter[title]=%25助手%25 （'%25'为'%'的转义） 
  + sort -modified(从新到旧) | modified(从旧到新)       
       
+ Response 200 (application/json)       

        {
          "meta": {
            "totalPages": 1,
            "totalElements": 1,
            "size": 5,
            "number": 1,
            "numberOfElements": 1,
            "first": true,
            "last": true,
            "sort": [
              {
                "direction": "DESC",
                "property": "modified",
                "ignoreCase": false,
                "nullHandling": "NATIVE",
                "descending": true,
                "ascending": false
              }
            ]
          },
          "links": {
            "self": "/wxSeeds?filter[title:like]=%Midifa%&sort=-modified&page[number]=1&page[size]=5",
            "first": "/wxSeeds?filter[title:like]=%Midifa%&sort=-modified&page[number]=1&page[size]=5",
            "last": "/wxSeeds?filter[title:like]=%Midifa%&sort=-modified&page[number]=1&page[size]=5"
          },
          "data": [
            {
              "id": 32,
              "enabled": 1,
              "creator": 0,
              "modifier": 0,
              "articleSeedId": 157,
              "title": "Midifan",
              "wechatId": "",
              "biz": "MjM5MTA1NjMwMA=="
            }
          ]
        }

### 删除 [DELETE] /wxSeeds/{id}
+ Description
  + [MUST]  Authenticated
  + [MUST] ROLE_ADMIN 
+  Response 204

## 微信文章管理
+ Data
   +  articleTopicId (long) - 与 article topics 表中对应的id
   +  seedId (long) 
   +  type (int) - 主题类型 0:图文，1：视频，2：音视频混合
   +  title (String) - 标题
   +  content (String) - 内容
   +  author (String) - 作者
   +  postDate (date) - 发布时间
   +  top (int) - 是否头条 0:是，1：否
   +  original (int) - 是否原创 0:否，1：是
   +  enabled (int) - 启用/禁用
   +  reviews (int) - 浏览量
   +  thumbsUp (int) - 点赞数
   +  seedTitle (String) - 公众号名
   +  creator (long) - 创建人
   +  modifier (long) - 修改人
   +  created (date) - 创建时间
   +  modified (date) - 修改时间

### 列表[GET]/topics?filter[seedId]=1&filter[modified:like]=%252018-05-03%25&fields[Topics]=id,title,seedId,original,postDate,modified,created
+ Parameters
  + id 
  + seedId
  + title
  + modified 这个必须使用模糊查询，格式为yyyy-MM-dd，例如：2018-05-03
     + 模糊查询示例：filter[title]=%25助手%25 （'%25'为'%'的转义） 
  + sort -modified(从新到旧) | modified(从旧到新)   
+ fields （必须返回的字段，不填则返回全部）
    + id 必须
    + title 必须
    + seedId 必须
    + original 必须
    + postDate 必须
    + modified 必须
    + created 必须
+ Response 200 (application/json)

        {
          "meta": {
            "totalPages": 6,
            "totalElements": 11,
            "size": 2,
            "number": 1,
            "numberOfElements": 2,
            "first": true,
            "last": false,
            "sort": null
          },
          "links": {
            "self": "/topics?fields[Topics]=id,title,seedId,original,postDate,modified,created&filter[seedId]=1&page[number]=1&page[size]=2",
            "first": "/topics?fields[Topics]=id,title,seedId,original,postDate,modified,created&filter[seedId]=1&page[number]=1&page[size]=2",
            "next": "/topics?fields[Topics]=id,title,seedId,original,postDate,modified,created&filter[seedId]=1&page[number]=2&page[size]=2",
            "last": "/topics?fields[Topics]=id,title,seedId,original,postDate,modified,created&filter[seedId]=1&page[number]=6&page[size]=2"
          },
          "data": [
            {
              "id": 3812,
              "created": "2018-05-03 16:17:15",
              "modified": "2018-05-14 14:34:37",
              "seedId": 1,
              "title": "Tokyo热不热我不知道，我只知道最近黑胶热！",
              "postDate": "2018-04-20T14:48:43.000+0000",
              "original": 0,
              "reviews": 184,
              "thumbsUp": 0,
              "seedTitle": "AKAI雅佳乐园"
            },
            {
              "id": 3813,
              "created": "2018-05-03 16:17:16",
              "modified": "2018-05-22 18:49:34",
              "seedId": 1,
              "title": "贾老板用MPC在演唱会上帅了一把！",
              "postDate": "2018-04-18T07:23:07.000+0000",
              "original": 0,
              "reviews": 236,
              "thumbsUp": 1,
              "seedTitle": "AKAI雅佳乐园"
            }
          ]
        }

### 删除 [DELETE] /topics/{id}

+ Description
  + [MUST]  Authenticated
  + [MUST] ROLE_ADMIN 
+ Response 200

### 文章详情[GET] /topics/{id}
+ Description
    + [MUST] Authenticated
    + [MUST] ROLE_ADMIN
+ Response 200 (application/json)

        {
        "data": {
            "id": 1,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2018-04-27 16:37:11",
            "modified": "2018-05-23 14:31:11",
            "articleTopicId": 997312,
            "seedId": 2,
            "type": 0,
            "title": "知名无线音箱秘密提交上市申请 估值最高30亿美元",
            "titleHash": 5636961133973108502,
            "content": "内容",
            "author": "艾维音响网",
            "postDate": "2018-04-27T05:05:18.000+0000",
            "top": 0,
            "original": 0,
            "groupSign": 1527056915994,
            "reviews": 272,
            "thumbsUp": 2,
            "seedTitle": "艾维音响网"
        }
    }
  
## 地区后台管理
+ Data
    + id (Long) - ID
    + parentId (Long) - 父节点
    + title (String) - 区域名称
    + leaf (int) - 是否叶子节点 0：否，1：是
    + enabled (int) - 是否可用 
    + creator (Long) - 创建人
    + modifier (Long) - 修改人
    + created (date) - 创建时间
    + modified (date) - 修改时间
  
### 增加 [POST] /wxRegions 
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN
+ Parameters
    + title 必填
    + parentId 必填

+ Request (application/json)
    
        {
             "data":{
             	 "parentId":0,
                "title":"测试省"
              }
         }

+ Response 200 (application/json)

        {
            "data": {
                "id": 431,
                "type": "wxRegions"
            }
        }

### 修改 [PATCH] /wxRegions/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN
+ Parameters
    + title 必填
    + parentId 必填

+ Request (application/json)
           
        {
            "data":{
            "title":"测试xx省"
            }
        }

+ Response 200

### 列表 [GET] /wxRegions?filter[parentId]=5

+ Parameters
    +  filter[parentId]

+ Response 200 (application/json)
    
        {
        "meta": {
            "totalPages": 2,
            "totalElements": 11,
            "size": 10,
            "number": 1,
            "numberOfElements": 10,
            "first": true,
            "last": false,
            "sort": null
        },
        "links": {
            "self": "/wxRegions?filter[parentId]=97&page[number]=1&page[size]=10",
            "first": "/wxRegions?filter[parentId]=97&page[number]=1&page[size]=10",
            "next": "/wxRegions?filter[parentId]=97&page[number]=2&page[size]=10",
            "last": "/wxRegions?filter[parentId]=97&page[number]=2&page[size]=10"
        },
        "data": [
            {
                "id": 98,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "杭州市",
                "leaf": 1
            },
            {
                "id": 99,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "宁波市",
                "leaf": 1
            },
            {
                "id": 100,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "温州市",
                "leaf": 1
            },
            {
                "id": 101,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "嘉兴市",
                "leaf": 1
            },
            {
                "id": 102,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "湖州市",
                "leaf": 1
            },
            {
                "id": 103,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "绍兴市",
                "leaf": 1
            },
            {
                "id": 104,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "金华市",
                "leaf": 1
            },
            {
                "id": 105,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:24",
                "modified": "2018-06-08 13:49:24",
                "parentId": 97,
                "title": "衢州市",
                "leaf": 1
            },
            {
                "id": 106,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:25",
                "modified": "2018-06-08 13:49:25",
                "parentId": 97,
                "title": "舟山市",
                "leaf": 1
            },
            {
                "id": 107,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-08 13:49:25",
                "modified": "2018-06-08 13:49:25",
                "parentId": 97,
                "title": "台州市",
                "leaf": 1
            }
        ]
    }


### 查询地区详情 [GET] /wxRegions/{id}
+ Parameters
    + id 必填

+ Response 200 (application/json)
       
       {
        "data": {
            "id": 68,
            "enabled": 1,
            "creator": 0,
            "modifier": 0,
            "created": "2018-06-08 13:49:24",
            "modified": "2018-06-08 13:49:24",
            "parentId": 67,
            "title": "哈尔滨市",
            "leaf": 1
        }
    }



### 删除 [DELETE] /wxRegions/{id}
+ Description
    + [MUST] authenticated
    + [MUST] ROLE_ADMIN
+ Response 204

## 分类后台管理
+ Data
  + id (Long) - ID
  + title (String) - 公众号分类名
  + description (String) - 分类描述
  + enabled (int) - 是否可用 
  + creator (Long) - 创建人
  + modifier (Long) - 修改人
  + created (date)  - 创建时间
  + modified (date) - 修改时间

### 增加 [POST] /wxCategories
+ Description
    + [MUST] Authenticated
    + [MUST] ROLE_ADMIN
+ Parameters
    + title 必填
    + description 必填
+ Request (application/json)
   
        {
        	"data":{
        		"title":"不一样的类",
        		"description":"描述同样的事"
        	}
       }

+ Response 200 (application/json)

    {
    "data": {
        "id": 3,
        "type": "wxCategories"
     }
    }
  
### 修改 [PATCH] /wxCategories/{id}
+ Description
+ [MUST] Authenticated
+ [MUST] ROLE_ADMIN

+ Parameters
    + title 必填
    + description 必填
+ Request (application/json)

        {
        	"data":{
        		"title":"不一样的xxx类",
        		"description":"描述同样的事xxx"
        	}
        }

+ Response 200
 
### 列表 [GET] /wxCategories

+ Response 200 (application/json)

        {
        "meta": {
            "totalPages": 1,
            "totalElements": 3,
            "size": 10,
            "number": 1,
            "numberOfElements": 3,
            "first": true,
            "last": true,
            "sort": null
        },
        "links": {
            "self": "/wxCategories?page[number]=1&page[size]=10",
            "first": "/wxCategories?page[number]=1&page[size]=10",
            "last": "/wxCategories?page[number]=1&page[size]=10"
        },
        "data": [
            {
                "id": 1,
                "enabled": 0,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-25 00:00:00",
                "modified": "2018-06-25 15:38:37",
                "title": "哈哈哈类",
                "description": "哈哈描述"
            },
            {
                "id": 2,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-25 15:37:17",
                "modified": "2018-06-25 15:37:17",
                "title": "加油类",
                "description": "添加描述"
            },
            {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-25 16:48:36",
                "modified": "2018-06-25 16:50:57",
                "title": "不一样的xxx类",
                "description": "描述同样的事xxx"
            }
        ]
    }

### 查询分类详情 [GET] /wxCategories/{id}
+ Parameters
    + id 必填
   
+ Response 200 (application/json)     
           
         {
            "data": {
                "id": 3,
                "enabled": 1,
                "creator": 0,
                "modifier": 0,
                "created": "2018-06-25 16:48:36",
                "modified": "2018-06-25 16:50:57",
                "title": "不一样的xxx类",
                "description": "描述同样的事xxx"
            }
          }

### 删除 [DELETE] /wxCategories/{id}

+ Description
    + [MUST] Authenticated
    + [MUST] ROLE_ADMIN
    
+ Response 200 
