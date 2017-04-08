#齐信OA接口文档#
	更新时间：2017年3月13日20:00:00
	更新内容：OA 接口的 第一版更新
##更新说明#
###更新时间2017年4月7日14:16###
	1、接口的部分返回形式的更改和更新
##<span id="1">请求地址说明</span>
例如

	url:http://oa.sdqixin.com/api.php?d=tash&m=login&a=checks
##<span id="1">接口返回说明</span>
返回的数据格式均为 json 格式，其中：
	
		code为 错误代码，200代表 返回正常  
		msg	为 提示信息，
		data为 返回的数据(可以为空)
	code为 200时代表返回正常，具体如下：
	
		201---apikey错误(接口APP的密钥)
		202---请求超时
		203---请求参数为空或者未传参数
		299---token 过期
##用户模块#
###1:用户登录##

	url： HOST/api.php?d=task&m=login&a=checks
	提交方式：post
	参数说明：	

|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|user    | 是    | 账号|
	|pass    | 是    | 密码|
	|timekey    | 是    | 当前时间戳 格式为 1458027682|
	|cfrom|是|appandroid(安卓)，appiphone（ios），client（客户端）|
	|device|否|设备码|
	|ip|否|登录ip地址|

	提交示例：
	url:
		HOST/api.php?d=task&m=login&a=checks
	data:
	{
	    "user":"qx000",
	    "pass":"123456",
		"timekey":"1458027682",
		"cfrom":"android/ios",
		"device":"设备码",//非必须
		"ip":"127.0.0.1",//非必须
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	    "userid": "1",//用户id
	    "truename": "管理员",//用户姓名
		"deptid":"23",//所在部门id
	    "deptname": "开发部",//所在部门
		"ranking":"管理员",//职位
	    "headiconurl": "upload/2015-08/1440578146698_4091.jpg",//头像
	    "token": "jtxztbd1",//提交请求所用的token
	    "apikey": "69463dfc59bfeb16aa082382b81fe02f"//用户提交请求所用appapikey
	    "time": 1471329612,
	    "now": "2016-08-16 14:40:12"
	 
	}	
###2:修改密码

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：	
|参数名 | 是否必须 | 参数类型 | 说明 |
	|-----|:------:|----|----|
	|oldPassword     | 是    |   string   | 原密码 |
	|newPassword    | 是    |    string   | 密码   |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "oldPassword":"123456", 
	    "newPassword":"nihao123",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}	
###3:修改姓名

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|truename    | 是    | 姓名

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "truename":"张三",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}	
###4:修改性别

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|sex    | 是    | 性别	

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "sex":"男",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}	
###5:修改工号

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|jobCode    | 是    | 工号	

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "jobCode":"QX110",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}		
###6:修改联系方式

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 参数类型 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | int    | 修改的用户id|
	|contactList    | json数组字符串    | 联系方式	
	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "contactList":
			[{“type”:1,”number”:”18615115727”}
			,{“type”:2,”number”:”3124543”}]	
		 
	}
	注: type: 1->手机  对应表中字段mobile
		 	  2->座机  对应表中字段tel

	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}	
###7:修改邮箱

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|email    | 是    | 邮箱	

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "email":"825822898@qq.com",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}
###8:修改地址

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|address    | 是    | 地址	

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "address":"淄博市张店区先进陶瓷创业园",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}
###9:修改生日

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|birthday    | 是    | 出生日期

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "birthday":"1990-04-01",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}
###10:修改籍贯

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|jiguan    | 是    | 籍贯	

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "jiguan":"山东省淄博市淄川区",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}
###11:修改民族

	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	|minzu    | 是    | 民族	

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "minzu":"汉",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}
###12:修改家庭住址
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	| homeAddress   | 是    | 家庭住址	

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "homeAddress":"张店区中润大道168号",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}
###13:修改入职日期
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|modifiedUserId   | 是    | 修改的用户id|
	| entryDate   | 是    | 入职日期

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "modifiedUserId":"1", 
	    "entryDate":"2016-10-15",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",  
	}
###14个人信息详情
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	| otherUserId | 是    | 用户id|
	
	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "otherUserId":"1", 
	}
	返回成功示例：
	{
		 “code”: 200,
	     ”msg”: ”成功”,
		 ”publicinfo”: {
		        “headiconurl”: ”头像地址”,
		        ”truename”: ”姓名”,
				“registphone”:”手机号”,
		        ”sex”: ”1”,
				“departmentid”:”部门id”,
		        ”departmentname”: ”部门名称”,
		        ”positionname”: ”职位名称”,
		        ”jobcode”: ”工号”,
			    ”contactlist”: [
		            {
		                “type”: 1,
		                ”number”: ”18615115724”
		            }
			    ],
		        ”email”: ”邮箱”,
		        ”address”: ”地址”
		    },
	    ”privateinfo”: {
	        "birthday": "2015-6-3",
	        "jiguan": "籍贯",
	        "minzu": "民族",
	        "homeaddress": "家庭住址",
	        "entrydate": "入职日期",
	       }
	}
###15:查看公司人员组织结构数据
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	| departmentId | 否    | 部门id(当==null时,表示获取最顶层的部门结构)|

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "departmentId":"1", 
	}	
	返回成功示例：
	{
	    “code”: 200,
	    ”msg”: ”成功”,
	    ”departmentlist”: [
	        {
	            "id": "32",
	            "name": "综合管理中心"       
	        }
	    ],
	    ”userlist”: [
	        {
	            "id": "11",
	            "headiconurl": "用户头像地址",
	            "truename": "姓名",
	            "positionname": "职位"
	        }
	    ]
	}
###16:通过姓名/电话搜索成员
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	| keyword | 否    | 查询关键词，姓名/电话模糊查询 |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{
	    "keyword":"张三/15963314123", 
	}	
	返回成功示例：
	 {
	    “code”: 200,
	    ”msg”: ”成功”,
	     ”userlist”: [
	        {
	            "id": "11",
	            "headiconurl": "用户头像地址",
	            "truename": "姓名",
	            "positionname": "职位"
	        }
	    ]
	}
###17:创建小组
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupName | 是   | string  |小组名称 |
	| groupIcon    | 是    | string | 小组头像地址 |
	| isAllMember    | 是    |  int |是否选择全部成员 1:是,0:否|
	| userList    | 是    | json数组字符串 | [“3”,”54”,”33”]
	用户id |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{   "groupName ":"讨论小组",
	    "groupIcon":"张三/15963314123", 
		"isAllMember":0,
		"userList":[“3”,”54”,”33”],
	}
	返回成功示例:
	{
			“code”:200,
			”msg”:”成功”,
			”id”:”232”     
	}
	注：默认创建的小组是私密小组
###18:我加入的小组列表
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| userId | 是   | int  |  用户id |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "userId ":1,
	}
    返回成功示例:
      
	“code”:200,
	”msg”:”成功”,
	list”:
		[
			{
			“id”:”32”,
			”headicon”:”头像地址”,
			”name”:”组名称”,
			”ywid”:”云旺群id”
			}
		]
	} 
###19:公开小组列表 
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明： 无

	返回成功示例: 
	{
		“code”:200,
		”msg”:”成功”,
		”list”: [
	        {
	            “id”: ”32”,
	            ”headicon”: ”头像地址”,
	            ”name”: ”组名称”,
	            ”ywid”:”云旺群id”,
	            ”isjoined”: 1   //我是不是已经加入了这个小组  ,1:已加入  0：未加入
	        }
		  ]
	}
###20:小组详情信息
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId ":1,
	}
	返回成功示例：
    {
	    “code”: 200,
	    ”msg”: ”成功”,
	    "name": "小组名称",
		"headicon": "小组头像",
		“type”:1，//公开还是私密小组  ，0：私密 1：公开
	    "groupheaduserid": "小组组长用户id",
	    "groupheaduser": "组长姓名",
		"groupheadheadicon": "组长头像",
		 ”isjoined”: 1   //我是不是已经加入了这个小组  ,1:已加入  0：未加入
	    "membercount": 4
	}
###21:加入小组
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| userId | 是   | int  |  用户id |
	| groupId | 是   | int  |  小组id |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "userId ":1,
		 "groupId":22,
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”,
	}
###22:该小组下的用户列表
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |

	返回成功示例:
	 {
		“code”,
		”msg”:”成功”,
		”header”:
			{
				“id”:”2”,
				”truename”:”姓名”,
				”departmentname”:”部门名称”,
				”positionname”:”职位名称”,
				”headiconurl”:”头像地址”
			},
		”memberlist”:
			[
				{
					“id”:”12”,
					”truename”:”姓名”,
					”departmentname”:”部门名称”,
					”positionname”:”职位名称”,
					”headiconurl”:”头像地址”,
				}
			]
	}
###23:小组中添加成员
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |
	| isAllMember | 是   | int  |  是否选择全部成员 1:是,0:否 |
	| userList | 是   | json数组字符串  |  [“3”,”54”,”33”]  用户id |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId  ":1,
		 "isAllMember":0,
		 "userList":[“3”,”54”,”33”],
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”
	}
###24:小组中移除成员
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |
	| removedUserId | 是   | int  | 要移除的用户id |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId  ":1,
		 "removedUserId":18,
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”
	}
###25:设置小组的状态(私密/公开)
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |
	| type | 是   | int  | 0:私密,1:公开 |

	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId  ":1,
		 "type":1,
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”
	}
###26:解散小组
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |
	
	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId  ":1,
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”
	}
###27:修改小组名称
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |
	| groupName | 是   | int  |  小组名称 |
	
	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId  ":1,
		 "groupName":"讨论组",
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”
	}
###28:修改小组头像
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |
	| groupIcon | 是   | int  |  小组头像地址 |
	
	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId  ":1,
		 "groupIcon":"upload/...",
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”
	}
###29:小组转让给其他用户
	url： HOST/api.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型  | 说明 |
	|-----|:------:|----|
	| groupId | 是   | int  |  小组id |
	| assignToUserId | 是   | int  |  交接用户id |
	
	提交示例：
	url:HOST/api.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "groupId  ":1,
		 "assignToUserId":66,
	}
	返回成功示例:
	{
		“code”:200,
		”msg”:”成功”
	}
##应用中心##
		应用中心包括以下应用
		1.今日会议
		2.通知公告
		3.工作日报
		4.考勤中心
		5.流程单据待办
		6.流程单据查看
		7.站内提醒
		8.单据申请	
		以下为具体的请求方式以及参数
###今日会议###
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式 post
	参数说明
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id (int)|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳 格式 int 1458027682|

	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	data:
	{  
		 "userId":1,
		 "token":65j13123tr,
		 "cfrom":"appandroid",
		 "appapikey":"hdfakddak1321345",
		 "timekey":1458027682
	}

	返回成功示例
	{
    "code":200,
    "msg":"成功",
    "hytitle":"[今日]2016-08-17(周三)",//会议ri
    "hycontent":[
        {
            "type":"会议",
            "hyname":"会议室1",  //会议室名
            "title":"[会议室1]每天部门工作汇报",
            "titles":"每天部门工作汇报", //会议标题
            "joinname":"开发部", //参会人
            "state":"正常</font>",//状态
            "status":"0",
            "startdt":"09:30:00至10:30:00", //时间
            "starttime":1471397400,
            "endtime":1471401000
        },
        {
            "type":"会议",
            "hyname":"会议室2",
            "title":"[会议室2]这么o",
            "titles":"这么o",
            "joinname":"开发团队,管理部,行政人事,开发部,商务部,财务部,业务部",
            "state":"正常</font>",
            "status":"0",
            "startdt":"16:00:00至16:30:00",
            "starttime":1471420800,
            "endtime":1471422600
        },
     ]
     
	}
###通知公告###
####通知公告列表</span>
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id int|
	|type|是| 我发出/我收到的  0:我收到的通知公告,1:我创建的通知公告|	
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳 格式 int 1458027682|
	|stype|否|默认为0 可传参数 0/1 0代表全部 1代表未读|

	提交示例：参考上面示例
		
	返回成功示例：
		{
		    "code": "200",
		    "msg": "",
			"wdshu": "1" 未读总数
		    "data": {
		        [
		            {
		                "id": "8",
		                "typename": "技术考核",公告类型
		                "title": "当月2016-03技术KPI考核",标题
		                "optdt": "2016-02-27 11:32:50",创建时间
						"optname":"管理员",   //创建人
		                "wd": "1" 未读
		            },
		            {
		                "id": "14",
		                "typename": "通知公告",
		                "title": "最新版本V2.2.7版本上线",
		                "optdt": "2016-02-26 21:58:24",
						"optname":"管理员",   //创建人
		                "wd": "0" 已读
                   },
        	   ] 	
    	}
	}
####通知公告详情
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：

|参数名 | 是否必须 | 说明|
		|-----|:-----:|-----|
		|id|是|通知id int|

	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
        "id": "14",
        "title": "最新版本V2.3.1版本上线",//标题
        "typename": "通知公告",//类型名称
        "content": "\n\t版本更新了很多内容\n</p>\\n\t1、添加了可自定义模块元素，录入元素。\n</p>\n\n\t2、无需写任何代码即可开发一个流程模块出来喽，详情</a> \n</p>\n\n\t \n</p>",//内容
        "enddt": null,//开始时间
        "startdt": null,//截止时间
        "optid": "1",
        "optname": "管理员",//创建人
        "optdt": "2016-05-08 10:19:52",
        "zuozhe": "RockOA开发团队",//作者
        "indate": "2016-05-08",//时间
        "receid": "u1,u61",//接收者id   (部门:d5,人员u1,u61)
        "recename": "管理员,张三",//接收者
        "status": "1"    
	}	
####发布通知公告
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：

|参数名 | 是否必须 |参数类型| 说明|
		|-----|:-----:|-----|----|
		|title|是|string|通知标题|
		|content|是|string|通知内容|
		|imageList|是|json数组字符串|图片
		|isSendToAllUser|是|int| 0:代表发送给部分成员,1:代表发送给全体成员
		|sendToUserList|否||发送的用户，当发给全体时，此字段为空[{“type”:1,”id”:”22”},{“type”:2,”id”:”11”}] 备注:  type:1  用户   id:用户id .  	type:2  部门   id：部门id   
	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	data:
	{	
		"userId":1,
	    "title":"会议", 
	    "content":"今下午例会15:00开始",
		"imageList":图片地址/文件,
		"isSendToAllUser":0,
		"sendToUserList":[{“type”:1,”id”:”22”},{“type”:2,”id”:”11”}],
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",
	}	  
####删除通知公告
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 |参数类型| 说明|
		|-----|:-----:|:-----:|----|
		|id|是|int|通知id|
	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	data:
	{	
		"id":53,
	}
		返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",
	}	  
###工作日报
####新增工作日报
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式 :post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id |
	|type|是| 日报类型,默认为0 |
	|content|是|内容|
	|plan|否|明日计划|
	|filename|否|上传文件名称|
	|filepath|否|上传文件路径|
	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	data:
	{	
		"userId":53,
		"type":0,
		"content":"今天汇总公司资料",
		"plan":"明天开车去济南开会",
		"filename":,
		"fileplan":,
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",
	}
####我的工作汇报列表
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式 :post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id |
	|dt|否| 为空时默认为全部日报,不为空时为指定哪一天 |
	|pageNo|是| 第几页,例如1,2,3 |
	|pageSize|是| 每页多少条记录,默认为20 |
	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	data:
	{	
		"userId":53,
		"dt":"2017-02-28",
		"pageNo":1,
		"pageSize":20	
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",
		'did':日报id,
		"dt":日报日期,
		"userId":用户id,
		"username":用户名
	}
####工作汇报详情
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式 :post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id 
	|id|是| 日报id 	
 
	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	data:
	{	
		"userId":53,
		"id":12
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",
		'did':12,     //日报id
		"dt":"2016-06-27",    //日报日期
		"adddt":"2016-06-27 17:29:14"   //新增时间
		"userId":1,      //用户id
		"username":"张三",    //用户名
		"content":"今天去拜访了济南的1个客户,预计下月能签合同",    //日报内容
		"plan":"明天继续跟进计划",(可以为空)				//明日计划
		"file":[
			{
				"filename":'张三的工作汇报',    //上传附件名称
				"filepath":'upload/2017-03/20170302182651_41050.doc',  //文件路径
			}
		]	
	}
###考勤中心
####初始化考勤数据
	url:HOST/api.php?d=tash&m=kaoqin&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型 |说明|
	|-----|:------:|:----:|----|
	|userId|是| int | 用户id |
	
	
	提交示例：
	url:HOST/api.php?d=tash&m=kaoqin&a=方法名
	data:
	{	
		"userId":53,		
	}
	返回成功示例
	{
	    "code":"200",
	    "msg":"成功",
		"attendancetime":"需要当天考勤的时间戳",
		"list":[
			{
				"type":"1", //考勤类型  1：上班考勤,2:下班考勤
				"status":0,//0:未打卡,1:已过期,2:未开始,3:已打卡,4:不用打卡
				"time":"08:00",//需要考勤的时间
				"signtime":"07:58",//打卡的时间 (只有在状态为已打卡的时候才有效)
			},
			{
				"type":"2", //考勤类型  1：上班考勤,2:下班考勤
				"status":2,//0:未打卡,1:已过期,2:未开始,3:已打卡,4:不用打卡
				"time":"17:30",//需要考勤的时间
				"signtime":"17:45",//打卡的时间 (只有在状态为已打卡的时候才有效)
			},
		]
	}
####定位打卡
	url:HOST/api.php?d=tash&m=kaoqin&a=adddkjl
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id int|
	|type|是|1:上班打卡   2:下班打卡 |
	|ip|是|手机登录ip地址 |
	|latitude|是|纬度 |
	|longitude|是|经度 |
	|address|是|地址 |
	
	提交示例：
	url:HOST/api.php?d=tash&m=kaoqin&a=adddkjl
	data:
	{	
		"userId":53,
		"type":1,	
		"latitude":"38.65777",
		"longitude":"104.08296",
		"address":"淄博市张店区先进陶瓷创业园",
		
	}
	返回成功示例
	{
	    "code":"200",
	    "msg":"成功"
	}
###流程单据待办###
####单据待办列表
	url:HOST/api.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id int|
	提交示例：
	url:HOST/api.php?d=tash&m=模块名&a=方法名
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",
        "totalCount": 1,   //总数
        "rows": [
            {    
				"id":"152",  //单据id
                "sericnum": "KA-20170204-0001",//单据号
                "modename": "请假条",
                "tablename": "kqinfo",
                "summary": "事假:2015-10-27 19:12:00至 2015-10-28 19:12:00共 	8.0小时,121212",//摘要
                "uid": "3",
                "mid": "51",
				"modeid":"66",
                "optdt": "2015-12-27 19:12:36",
                "applydt": "2015-12-27",//申请日期
                "statusman": "待大乔处理</font>",//状态
                "nowcheckid":"步骤审核人id",
				"nowcheckname":"步骤审核人姓名",
                "username": "张三",//申请人
                "deptid": "13", //部门id
				"deptname": "综合运营部", //部门名称
            }
        ]   
	}
####<span id="1.1.3">删除单据</span>####
	url:HOST/api.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id int|
	|id|是| 单据id int|
	提交示例：
	url:HOST/api.php?d=tash&m=模块名&a=方法名
	data
	{	
		"userId":1,
		"id":152,
	}
	返回成示例：
		{
		    "code": 200,
		    "msg": "成功"
		}
	注:数据表qixin_flow_bill表中改变字段isdel的状态
####<span id="1.1.2">处理单据</span>
	url:HOST/api.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 参数类型 |说明|
	|-----|:------:|:----:|----|
	|userId|是| int|用户id |
	|id|是| int|单据id int|
	|zt|是| int|处理单据的状态 1:通过,2:不通过|
	|remark|是| string|备注,不通过时为必填项(不通过原因),通过时可以选填|
	提交示例：
	url:HOST/api.php?d=tash&m=模块名&a=方法名
	data
	{	
		"userId":1,
		"id":152,
		"zt":2,
		"remark":"数据不正确,请再次确认",
	}
	返回成功示例：
	{
	    "code": 200,
		"msg":"成功"
	}
####<span id="1.1.1">单据待办详情</span>
	url:HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
		|-----|:------:|----|
		|userId|是| 用户id   (int 类型)|
		|token|是| 用户登录成功后返回的token |
		|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
		|timekey|是| 时间戳 格式 int 1458027682|
		|appapikey|是|登录成功返回的|
		|id|是|单据id|
	提交示例：
	url:HOST/index.php?d=task&m=模块名&a=方法名
	返回成功示例：	
    {
	    "code": 200,
	    "msg": "",
        "info": {
            "id": "51",
            "uid": "3",
			"table":"goodm",    //数据库表
			"sericnum":"CAR-20161208-0001", //流程单号
            "modename": "请假条",//类型
			"modeid":57,  //模块流程id
			"mid":1,      //模块流程下的编号
            "optid": "3",
            "optdt": "2015-12-27 19:12:36",
			"optname":"管理员",
            "status": "0",//审核中  1代表审核成功 2审核未通过
            "nowcheckid": "4",		//当前步骤审核人id
            "allcheckid": "4,3",  //所有审核人id
			"isdel":0,       	 //是否删除状态
            "nstatus": "0",       //当前状态值
			"nowcheckid":120,  //当前审核人id
            "nowcheckname": "大乔",
			"checksm":"最后审核意见",
            "applydt": "2015-12-27",   //申请时间
     	   },
        "log": [   //审核记录
            {	
				"stepname":"事业群负责人",
				"checkid":12,
                "checkname": "张三",
                "zt": 1// 	状态,1代表通过,2代表不通过
            },
            {
               "stepname":"综合管理中心法务",
				"checkid":14,
                "checkname": "李四",
                "zt": 2// 	状态,1代表通过,2代表不通过
            }
      	  ],
        "readarr": [//查阅记录
            {
                "uid": "4",//用户id
                "optdt": "2016-08-16 15:28:18",//时间
                "stotal": "2",//次数
                "username": "王武",//姓名
                "face": "images/noface.jpg"//头像
            },
			{
                "uid": "78",//用户id
                "optdt": "2017-03-17 12:42:30",//时间
                "stotal": "2",//次数
                "username": "大乔",//姓名
                "face": "images/noface.jpg"//头像
            }
        ],
        "file": [],//相关文件
        "content": ""
	}
###单据查看###
####单据查看列表
	单据查看共分为五类单据，分别是 我的申请、经我处理、我下属申请、未通过、待处理	
	url:http://HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id|
	|pageNo|是|分页页码,例如1,2,3|
	|pageSize|是|分页条数,例如20,30,40|
	|atype|否|类型，默认为0 0代表我的申请 1代表经我处理 2代表我下属申请 3代表授权查看 4代表未通过 5代表待处理|
	提交示例：
	url:HOST/api.php?d=tash&m=模块名&a=方法名
	返回成功示例：	
		{
		    "code": 200,
		    "msg": "",
		    "data":[
		          	 {
		                "id": "39",
		                "sericnum": "PA-20150909-0001", 单据流程编号
		                "table": "fininfom",
		                "mid": "2",
		                "modeid": "11",
		                "modename": "费用报销",
		                "uid": "1",
		                "optdt": "2015-09-09 10:35:35",
		                "optid": "1",
		                "optname": "管理员",
		                "allcheckid": "7,9,10",
		                "isdel": "0",
		                "nstatus": "2",
		                "applydt": "2015-09-09",
		                "nstatustext":"待岳方处理",
		                "username": "管理员",
		                "deptname": "开发部",
		                "statustext": "赵子龙审核不通过</font>,待赵子龙处理</font>",
		                "modenum": "finfybx",
		                "summary": "报销金额:15.00"
		           	 }
		      	 ]
		}	
####单据查看详情
[与单据待办详情相同](#1.1.1)
####单据处理
[与单据待办处理相同](#1.1.2)
####单据删除
[与单据待办删除相同](#1.1.3)
###站内提醒###
####站内提醒列表
	url:http://HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id  (int类型)	
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳 格式 1458027682|
	提交示例：
	url:http://HOST/index.php?d=task&m=模块名&a=方法名
	返回成功示例：	
		{
		    "code": 200,
		    "msg": "成功",
		    "data": [
		        {
		            "title": "工作任务",
		            "mess": "[管理员]分配一条[研究]工作任务:测试 站内提醒",
		            "status": "1",//状态0 为未读  1为已读
		            "optdt": "2016-07-13 09:42:36",
		            "id": "19",  
					"uid":1,   //用户id
		            "mid": "16"
		        },
		        {
		            "title": "加班单",
		            "mess": "您提交的[加班单,单号:KJ-20160423-0001]已全部处理完成",
		            "status": "1",
		            "optdt": "2016-04-27 21:47:24",
		            "id": "1",
					"uid":1,   //用户id
		            "mid": "57"
		        }
		    ]
		    
		}
####站内提醒详情
[与单据待办详情相同](#1.1.1)
###单据申请
####单据申请列表
	url:http://HOST/index.php?d=task&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id |
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳 格式 1458027682|
	|appapikey|是|登录成功返回的|
	提交示例：
	url:http://HOST/index.php?d=task&m=模块名&a=方法名
	data:
	{
		"userId":1,
		"token":"1231lkhfsyr",
		"cfrom":"appandroid",
		"timekey":"1458027682",
		"appapikey":"1l3k13h1k45h1k5hk14k1h4",
	}
	返回成功示例：
	{
		"code": 200,
		"msg": "成功",
		"data": [
			        {
			            "num": "leave",
			            "name": "请假条",
			            "type": "人力",
			            "sort": "0"
			        },
			        {
			            "num": "waichu",
			            "name": "外出出差",
			            "type": "人力",
			            "sort": "2"
			        },
			        {
			            "num": "meet",
			            "name": "会议预定",
			            "type": "行政",
			            "sort": "8"
			        },
			        {
			            "num": "gong",
			            "name": "通知公告",
			            "type": "行政",
			            "sort": "9"
			        }      
		  	  ]	  
		}
####请假条####
#####提交请假条#####
	url:http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式： post
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|userId|是| 用户id |
	|timekey|是| 时间戳   1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的|
	|qjkind|是|请假类型分为 事假、病假
	|stime|是|开始时间 格式为 2016-03-10 16:01:00
	|etime|是|结束时间 格式为 2016-03-10 16:01:00
	|totals|是|总时长
	|explain|是|说明
	提交示例：
		url:http://HOST/index.php?d=tash&m=模块名&a=方法名
		data：
			{	
				"userId":1,
				"token":"1231lkhfsyr",
				"cfrom":"appandroid",
				"timekey":"1458027682",
				"appapikey":"1l3k13h1k45h1k5hk14k1h4",
			    "qjkind": "病假",
			    "stime": "2016-03-14 11:01:01",
			    "etime": "2016-03-15 8:00:00",
			    "totals": "24",
			    "explain": "身体不舒服"
			}
		返回成功示例：
		{
		    "code": 200,
		    "msg": "成功", 
		}
#####获取请假时间差
	url:http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳   1458027682|
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的
	|stime|是|开始时间 格式为 2016-03-10 16:01:00
	|etime|是|结束时间 格式为 2016-03-10 16:01:00
	提交示例：
	url:http://HOST/index.php?d=tash&m=模块名&a=方法名
	返回成功示例：
	{
	    "code": 200,
	    "msg": "成功",
	    "data": 8,   //8小时
	}
####外出出差
	url:http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的
	|atype|是|外出类型 选项为 外出、出差
	|outtime|是|外出时间 格式为 2016-03-10 16:01:00
	|intime|是|预计回岗 格式为 2016-03-10 16:01:00
	|address|是|外出地址
	|reason|是|外出事由
	|explain|否|说明
	提交示例：
		http://HOST/index.php?d=tash&m=模块名&a=方法名
		data：
			{
				"userId":1,
				"token":"1231lkhfsyr",
				"cfrom":"appandroid",
				"timekey":"1458027682",
				"appapikey":"1l3k13h1k45h1k5hk14k1h4",
				"atype": "外出",
			    "outtime": "2016-03-14 11:01:01",
			    "intime": "2016-03-15 8:00:00",
			    "address": "淄博张店",
			    "reason": "外出",
			}
		返回成功示例：
			{
			    "code": 200,
			    "msg": "成功",
			}
####会议预定
#####获取会议室
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明:
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|adminid|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） 
	|appapikey|是|登录成功返回的
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	返回示例：
	{
	    "code": 200,
	    "msg": "成功",	  
	    "hyname": 
			[
	            {
	                "name": "会议室1"
	            },
  			  	{
	                "name": "会议室2"
	            },
				{
	                "name": "会议室3",
	            }
	        ]  
	}
#####会议室预定
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的
	|hyname|是|会议室名 如：会议室1
	|title|是|会议主题
	|startdt|是|会议开始时间 格式为2016-07-14 11：00：00
	|enddt|是|会议结束时间 格式为2016-07-14 11：00：00 
	|istz|否|是否到时提醒 0:表示不提醒 1:表示提醒  默认为0
	|joinname|是|示例：行政人事,管理员,商务部
	|joinid|是|示例：d3,u1,d5
	|explain|否|说明
**注：joinid中： d3表示部门id为3的人，u1表示用户id为1的人**
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"
		   
		}
####车补报销
#####车辆补贴月报
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的
	|carcode|是|车牌号 如：鲁C 88888	
	|startkm|是|起始里程 75000
	|endkm|是|结束里程 80000
	|chazhi|是| 补贴里程  5000
	|explain|否|说明

	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}
####非业务合同
#####审批签订
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的
	|contractnum|是|合同编号	
	|dt|是|签约日期  例如 "2017-03-16"
	|cname|是|客户名称 
	|ractname|是| 合同名称 
	|timelimit|是|合同期限
	|copies|是|签订份数 
	|money|是|合同金额
	|ztype|是| 支付方式
	|content|是| 合同内容
	|explain|否| 备注
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}
####行政档案
#####行政档案申请
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的	
	|isout|是|	借阅是否外带(0:否,1:是)
	|explain|是| 说明,申请具体档案的说明
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
			"isout":1,
			"explain":"申请法人的营业执照使用一下,潍坊大区需要使用1天,需要外带."
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}
####转正和离职
#####转正申请
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的	
	|ranking|是|	 职位
	|entrydt|是| 入职日期
	|pdt|是| 试用到期日
	|fdt|是| 转正日期
	|explain|是|申请说明
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
			"ranking":"高管",
			"entrydt":"2016-11-10",
			"pdt":"2017-02-10",
			"fdt":"2017-03-16",
			"explain":"试用期顺利完成项目,特申请转正,谢谢",
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}
#####离职类型初始化
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功",
			"data":
			[
				{
					"id":1,
					"name":"自动离职",
				},
				{
					"id":2,
					"name":"退休",
				},
				{
					"id":3,
					"name":"生病辞职",
				},
				{
					"id":3,
					"name":"自己辞职",
				},
				{
					"id":4,
					"name":"公司辞退",
				}
			]  
		}
#####离职申请
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的	
	|ranking|是|	 职位
	|entrydt|是| 入职日期
	|type|是| 离职类型
	|leavedt|是| 离职日期
	|reason|是|离职原因
	|explain|否|备注
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
			"ranking":"高管",
			"entrydt":"2016-10-11",
			"type":"自己辞职",
			"leavedt":"2017-03-15",
			"reason":"个人原因",
			"explain":"备注可为空"
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}
####资格证书
#####资格证书补贴申请
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户(申请人)id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的	
	|cname|是| 证书名称
	|takedt|是| 取证时间
	|signdt|是| 注册到公司时间
	|allowance|是| 补贴标准/元
	|performdt|是|执行时间
	|expiredt|是|到期时间
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
			"cname":"职称/资格",
			"takedt":"2017-03-16 11:37:45",
			"signdt":"2017-02-14 10:30:52",
			"allowance":"3千",
			"performdt":"2017-03-12 11:12:30",
			"expiredt":"2017-03-28 08:30:21",
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}
####物品采购和领用
#####物品列表初始化数据
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的		
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功",
			"data":
				[
					{
						"id":4,
						"typeid":63,		
						"name":"台式机主机",
					},
					{
						"id":5,
						"typeid":63,		
						"name":"键盘",
					},
					{
						"id":6,
						"typeid":63,		
						"name":"鼠标",
					},
					{
						"id":7,
						"typeid":63,		
						"name":"显示器",
					},
					{
						"id":8,
						"typeid":63,		
						"name":"U盘",
					},
					{
						"id":9,
						"typeid":63,		
						"name":"无线网卡",
					},
					{
						"id":10,
						"typeid":63,		
						"name":"电话座机",
					}	
				]	   
		}
#####物品领用
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户(申请人)id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的	
	|applydt|是| 申请日期
	|goods|是| 领用物品   参数类型:json数组
	|explain|否|说明
	
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
			"applydt":"2017-03-16",
			"goods":
				[
					{
						"id":3,  		//	物品id
						"name":"鼠标", //物品名称	
						"count":1,    //数量
						"unit":"个",   //单位
					},
					{
						"id":4,  		//	物品id
						"name":"摄像机", //物品名称
						"count":3,    //数量
						"unit":"台",   //单位
					}

				]
			"explain":"办公用品不够了",     //说明
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}
#####物品采购
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	提交方式：post
	参数说明：
|参数名 | 是否必须 | 说明
	|-----|:------:|----|
	|userId|是| 用户(申请人)id 
	|timekey|是| 时间戳 1458027682
	|token|是| 用户登录成功后返回的token 
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端）
	|appapikey|是|登录成功返回的	
	|applydt|是| 申请日期
	|supplier|是|供应商
	|goods|是| 领用物品   参数类型:json数组
	|explain|否|说明
	
	
	提交示例：
	http://HOST/index.php?d=tash&m=模块名&a=方法名
	data：
		{
			"userId":1,
			"token":"1231lkhfsyr",
			"cfrom":"appandroid",
			"timekey":"1458027682",
			"appapikey":"1l3k13h1k45h1k5hk14k1h4",
			"applydt":"2017-03-16",
			"supplier":"科讯电子有限公司",
			"goods":
				[
					{
						"id":3,  		//	物品id
						"name":"鼠标", //物品名称	
						"count":1,    //采购数量
						"unit":"个",   //单位
						"price":"25.00"  //单价
					},
					{
						"id":4,  		//	物品id
						"name":"摄像机", //物品名称
						"count":3,    //数量
						"unit":"台",   //单位
						"price":"3750.50"  //单价
					}

				]
			"explain":"办公用品不够了",     //说明
		}	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "成功"	   
		}