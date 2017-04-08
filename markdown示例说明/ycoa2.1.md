#永昌物流OA接口文档#

	更新时间：2016年8月15日11:08:09
	更新内容：OA 接口的 第二版更新
##更新说明#
###更新时间2016年11月26日08:46:18###
	1、库存的接口的添加 在应用中心添加 库存查看功能
*[查看详情](#1)
###更新时间2016年8月22日10:04:42###
	1、登录的 接口返回错误信息 修改  token expire 为token过期，即为当前用户在该种设备上 被顶下线  错误代码为 299
*[查看详情](#1)

	2、组织结构的 返回 数据修改
*[查看详情](#8.1)	
###更新时间2016年8月20日08:48:35###
	1、单据申请中的  通知公告改为  信息公告 ，信息公告的分类 由接口 获取 
*[查看详情](#7.8.5)
###更新时间2016年8月17日14:24:00###
	1、单据详情  添加标记符  标记是否需要在详情页显示 “删除单据” “处理单据” “编辑单据”
		编辑单据 可暂时不做  
		单据详情的 固定内容为  base_name 、base_deptname 、base_flowname 、base_sericnum
			logstr 、checkstatustext
		其余内容的表头为 fields数组中的 值  可以通过fields中的 key 在data中 找到对应的值
		例如：
			"fields": {
            "qjkind": "请假类型",
            "stime": "开始时间",
            "etime": "截止时间",
            "totals": "请假(小时)",
            "explain": "说明"
        	},
		"data": {
            "id": "51",
            "uid": "3",
            "kind": "请假",//类型
            "qjkind": "事假",//请假类型
            "stime": "2015-10-27 19:12:00",//请假开始时间
            "etime": "2015-10-28 19:12:00",//请假结束时间
            "totals": "8.0",//请假总时长
            "optid": "3",
            "optdt": "2015-12-27 19:12:36",
            "explain": "121212",//说明
            "status": "0",//审核中  1代表审核成功 2审核未通过
            "remark": null,
            "checkstatustext": "待大乔处理</font>",//状态
            "base_name": "貂蝉",//姓名
            "base_deptname": "行政人事",//部门
            "base_flowname": "请假条",//模块名
            "base_sericnum": "KL-20151227-0002",//流程单号
            "base_summary": "事假:2015-10-27 19:12:00至2015-10-28 19:12:00共8.0小时,121212"//摘要
        },
		"logstr": "1. 主管审核(大乔)</span> → 2. 人事确认(貂蝉)</span>",//流程
		详情页的内容为
|姓名|貂蝉|
|:--|:---|
|部门|行政人事|
|模快|请假条|
|单号|KL-20151227-0002|
|请假类型|事假|
|开始时间|2015-10-27 19:12:00|
|截止时间|2015-10-28 19:12:00|
|请假(小时)|8.0|
|说明|121212|
|状态|待大乔处理</font>|
|流程|logstr|

*[查看详情](#7.1.2)
	
	2、通知公告 添加参数 stype stype默认为0 代表获取全部通知 1 代表未读通知
*[查看详情](#7.5.1)
###更新时间2016年8月16日17:38:06###
	1、聊天加接口
	2、上传文件接口修改
###更新时间2016年8月16日14:50:30###
	1、appapikey 为登录成功后返回
	2、删除单据中 ： sm 为必填 为删除原因
	3、单据处理中： sm为  不通过的原因 不通过时 必填
##<span id="1">接口返回说明</span>

	返回的数据格式均为 json 格式，其中：
	
		code为 错误代码，200代表 返回正常  
		msg	为 提示信息，
		data为 返回的数据
	code为 200时代表返回正常，具体如下：
	
		201---apikey错误
		202---请求超时
		299---token 过期
##登录##
	url： HOST/index.php?d=taskrun&m=login|appapi&a=checklogin&ajaxbool=true
	提交方式：post
	参数说明：		
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|user    | 是    | 用户名|
	|pass    | 是    | 密码|
	|timekey    | 是    | 当前时间戳 格式为 1458027682|
	|cfrom|是|appandroid(安卓)，appiphone（ios），client（客户端）|
	|device|否|设备码|
	|ip|否|登录ip地址|

	提交示例：
	url:
		http://tryworld.cn/index.php?d=taskrun&m=login|appapi&a=checklogin&ajaxbool=true&cfrom=appandroid&timekey=1471231907
	data:
	{
	    "user":"zilong",
	    "pass":"123456",
	}
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "uid": "1",//用户id
	        "name": "管理员",//用户姓名
	        "user": "admin",//用户名
	        "pass": "123456",//密码
	        "deptname": "开发部",//所在部门
	        "face": "upload/2015-08/1440578146698_4091.jpg",//头像
	        "token": "jtxztbd1",//提交请求所用的token
	        "splittime": 0,
	        "apikey": "69463dfc59bfeb16aa082382b81fe02f"//用户提交请求所用appapikey
	    },
	    "sysd": {
	        "time": 1471329612,
	        "now": "2016-08-16 14:40:12"
	    }
	}
##注销##
	url:HOST/index.php?d=taskrun&m=login|appapi&a=exitlogin&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 1458027682|
	|token|是|登录token|
	|cfrom|是|appandroid(安卓)，appiphone（ios），client（客户端）|
	|appapikey|是|登录成功返回的|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=login|appapi&a=checklogin&ajaxbool=true&a=exitlogin&timekey=1471330676&cfrom=appandroid&adminid=1&token=g128m5gi&appapikey=69463dfc59bfeb16aa082382b81fe02f
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": "success",
	    "sysd": {
	        "time": 1471330677,
	        "now": "2016-08-16 14:57:57"
	    }
	}
##首页初始化数据##
	url: HOST/index.php?d=taskrun&m=index|appapi&a=initdata&ajaxbool=true	
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 1458027682|
	|token|是|登录token|
	|cfrom|是|appandroid(安卓)，appiphone（ios），client（客户端）|
	|appapikey|是|登录成功返回的|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=index|appapi&a=initdata&ajaxbool=true&timekey=1471330904&cfrom=appandroid&adminid=1&token=g128m5gi&appapikey=69463dfc59bfeb16aa082382b81fe02f
	返回成功示例：
	{
	    "code":200,
	    "msg":"",
	    "data":[
	        {
	            "title":"单据待办",
	            "total":1,
	            "titles":"",
	            "icon":"webreim/client/images/im/daibans.png",
	            "num":"daiban",
	            "type":"bs",
	            "id":"0"
	        },
	        {
	            "title":"今日会议",
	            "total":0,
	            "titles":"",
	            "icon":"webreim/client/images/im/meet.png",
	            "num":"meet",
	            "type":"bs",
	            "id":"0"
	        },
	        {
	            "title":"RockOA客服",
	            "total":"2",
	            "titles":"REIM人员信息,[07-16 09:25]",
	            "icon":"upload/2015-08/24_1510166137.png",
	            "num":"user_2",
	            "type":"user",
	            "id":"2"
	        },
	        {
	            "title":"刘备",
	            "total":"10",
	            "titles":"REIM人员信息,[07-28 16:26]",
	            "icon":"images/noface.jpg",
	            "num":"user_7",
	            "type":"user",
	            "id":"7"
	        },
	        {
	            "title":"哈哈哈",
	            "total":"4",
	            "titles":"REIM讨论组信息,[08-12 16:38]",
	            "icon":"images/im/taolun.png",
	            "num":"taolun_8",
	            "type":"taolun",
	            "id":"8"
	        },
	        {
	            "title":"站内提醒",
	            "total":0,
	            "titles":"",
	            "icon":"webreim/client/images/im/tixings.png",
	            "num":"todo",
	            "type":"bs",
	            "id":"0"
	        },
	        {
	            "title":"通知公告",
	            "total":0,
	            "titles":"",
	            "icon":"webreim/client/images/im/gong.png",
	            "num":"gong",
	            "type":"bs",
	            "id":"0"
	        },
	        {
	            "title":"工作任务",
	            "total":6,
	            "titles":"",
	            "icon":"webreim/client/images/im/renwu.png",
	            "num":"work",
	            "type":"bs",
	            "id":"0"
	        }
	    ],
	    "sysd":{
	        "time":1471330910,
	        "now":"2016-08-16 15:01:50"
	    }
	}
##首页同步数据##
	url:HOST/index.php?d=taskrun&m=index|appapi&a=initdex&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 1458027682|
	|token|是|登录token|
	|cfrom|是|appandroid(安卓)，appiphone（ios），client（客户端）|
	|appapikey|是|登录成功返回的|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=index|appapi&a=initindex&ajaxbool=true&timekey=1471331056&cfrom=appandroid&adminid=1&token=g128m5gi&appapikey=69463dfc59bfeb16aa082382b81fe02f
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "msg": "",
	        "total": {
	            "daiban": 1,
	            "todo": 0,
	            "meet": 0,
	            "reim": 24,
	            "work": 6,
	            "gong": 0
	        },
	        "reimarr": [
	            {
	                "type": "user",
	                "id": "2",
	                "stotal": "2",
	                "optdt": "2016-07-16 09:25:54",
	                "name": "RockOA客服",
	                "face": "upload/2015-08/24_1510166137.png"
	            },
	            {
	                "type": "user",
	                "id": "7",
	                "stotal": "10",
	                "optdt": "2016-07-28 16:26:36",
	                "name": "刘备",
	                "face": "images/noface.jpg"
	            },
	            {
	                "type": "taolun",
	                "id": "8",
	                "stotal": "4",
	                "optdt": "2016-08-12 16:38:33",
	                "name": "哈哈哈",
	                "face": ""
	            },
	            {
	                "type": "agent",
	                "id": "3",
	                "stotal": "6",
	                "optdt": "2016-07-25 14:12:30",
	                "name": "通知公告",
	                "face": "webreim/client/images/im/laba.png"
	            },
	            {
	                "type": "agent",
	                "id": "7",
	                "stotal": "2",
	                "optdt": "2016-07-15 11:24:31",
	                "name": "单据待办",
	                "face": "webreim/client/images/im/daibans.png"
	            }
	        ],
	        "titles": {
	            "listcheck": "",
	            "work": "未完成6条</font>"
	        }
	    },
	    "sysd": {
	        "time": 1471331057,
	        "now": "2016-08-16 15:04:17"
	    }
	}
##获取个人信息##
	url:HOST/index.php?d=taskrun&m=user|appapi&a=gereninfor&ajaxbool=true
	提交方式：get
	参数说明：
	
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 1458027682|
	|token|是|登录token|
	|cfrom|是|appandroid(安卓)，appiphone（ios），client（客户端）|
	|appapikey|是|登录成功返回的|
	|uid|否|int 用户id 默认为获取 adminid的信息|
	|appapikey|是|登录成功返回的|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=user|appapi&a=gereninfor&ajaxbool=true&timekey=1471331213&cfrom=appandroid&adminid=1&token=g128m5gi&appapikey=69463dfc59bfeb16aa082382b81fe02f
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "name": "管理员",//用户姓名
	        "user": "admin",//用户名
	        "deptname": "开发部",//部门
	        "ranking": "OA项目经理",//职位
	        "face": "upload/2015-08/1440578146698_4091.jpg",//头像
	        "companyid": "1",
	        "tel": "0135-2222222",//联系电话
	        "mobile": "15800000",//手机
	        "email": "admin@rockoa.com",//邮箱
	        "gender": "男",//性别
	        "company": "RockOA开发团队"//所在公司
	    },
	    "sysd": {
	        "time": 1471331214,
	        "now": "2016-08-16 15:06:54"
	    }
	}
##应用中心 ##
		应用中心包括以下应用
		1.单据待办
		2.今日会议
		3.考勤中心
		4.站内提醒
		5.通知公告
		6.单据查看
		7.工作任务
		8.单据申请
		
		以下为具体的请求方式以及参数
###单据待办###
####单据待办列表
	url:HOST/index.php?d=taskrun&m=flow|appapi&a=daiban&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 格式 int 1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=flow|appapi&a=daiban&ajaxbool=true&timekey=1471331892&cfrom=appandroid&adminid=4&token=pmdnqibo&appapikey=69463dfc59bfeb16aa082382b81fe02f
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "totalCount": 1,
	        "rows": [
	            {
	                "modenum": "leave",//
	                "modename": "请假条",
	                "tablename": "kq_info",
	                "summary": "事假:2015-10-27 19:12:00至2015-10-28 19:12:00共8.0小时,121212",//摘要
	                "uid": "3",
	                "mid": "51",
	                "optdt": "2015-12-27 19:12:36",
	                "applydt": "2015-12-27",//申请日期
	                "statusman": "待大乔处理</font>",//状态
	                "notbtnarr": {
	                    "1": [
	                        "通过",
	                        "1",
	                        0,
	                        0,
	                        "green"
	                    ],
	                    "2": [
	                        "不通过",
	                        "2",
	                        0,
	                        -1,
	                        "red"
	                    ]
	                },
	                "name": "貂蝉",//申请人
	                "deptname": "行政人事"//部门
	            }
	        ]
	    },
	    "sysd": {
	        "time": 1471334163,
	        "now": "2016-08-16 15:56:03"
	    }
	}
####<span id="7.1.2">单据待办详情</span>
	url:HOST/index.php?d=taskrun&m=flow|appapi&a=xiang&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
		|-----|:------:|----|
		|adminid|是| 用户id int|
		|token|是| 用户登录成功后返回的token |
		|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
		|timekey|是| 时间戳 格式 int 1458027682|
		|appapikey|是|登录成功返回的|
		|tablename|是|该参数在列表的json中 table|
		|mid|是|信息 mid 该参数在列表json中 mid int|
		|modenum|否|模块列表中的 num值|
	提交示例：
	http://www.ycoa.com/index.php?d=taskrun&m=flow|appapi&a=xiang&ajaxbool=true&timekey=1471333409&cfrom=appandroid&adminid=4&token=settpdr0&appapikey=69463dfc59bfeb16aa082382b81fe02f&modenum=leave&mid=51&tablename=kq_info
	返回成功示例：	
    {
	    "code": 200,
	    "msg": "",
	    "data": {
	        "data": {
	            "id": "51",
	            "uid": "3",
	            "kind": "请假",//类型
	            "qjkind": "事假",//请假类型
	            "stime": "2015-10-27 19:12:00",//请假开始时间
	            "etime": "2015-10-28 19:12:00",//请假结束时间
	            "totals": "8.0",//请假总时长
	            "optid": "3",
	            "optdt": "2015-12-27 19:12:36",
	            "explain": "121212",//说明
	            "status": "0",//审核中  1代表审核成功 2审核未通过
	            "isturn": "1",
	            "nowcheckid": "4",
	            "allcheckid": "4,3",
	            "nstatus": "0",
	            "statusman": null,
	            "nowcheckname": "大乔",
	            "optname": null,
	            "applydt": "2015-12-27",
	            "isxj": "0",
	            "sicksm": null,
	            "remark": null,
	            "checkstatustext": "待大乔处理</font>",//状态
	            "base_name": "貂蝉",//姓名
	            "base_deptname": "行政人事",//部门
	            "base_flowname": "请假条",//模块名
	            "base_sericnum": "KL-20151227-0002",//流程单号
	            "base_summary": "事假:2015-10-27 19:12:00至2015-10-28 19:12:00共8.0小时,121212"//摘要
	        },
	        "user": {
	            "name": "貂蝉",
	            "deptname": "行政人事"
	        },
	        "aurs": {
	            "name": "貂蝉",
	            "deptname": "行政人事"
	        },
	        "log": [
	            {
	                "name": "大乔",
	                "cname": "主管审核",
	                "zt": 1// 1代表通过  2代表不通过
	            },
	            {
	                "name": "貂蝉",
	                "cname": "人事确认",
	                "zt": 2
	            }
	        ],
	        "readarr": [//查阅记录
	            {
	                "uid": "4",//用户id
	                "optdt": "2016-08-16 15:28:18",//时间
	                "stotal": "2",//次数
	                "name": "大乔",//姓名
	                "face": "images/noface.jpg"//头像
	            }
	        ],
	        "logstr": "1. 主管审核(大乔)</span> → 2. 人事确认(貂蝉)</span>",//流程
	        "logarr": [],//审核记录
	        "ischeck": 1,//是否显示 审核  0代表不显示 1代表显示
	        "isdel": 0,//是否显示 删除单据  0代表不显示 1代表显示
	        "isedit": 0,//是否可以编辑
	        "actarr": [
	            [
	                "1",
	                "通过",
	                0
	            ],
	            [
	                "2",
	                "不通过",
	                -1
	            ]
	        ],
	        "status": "0",
	        "flownum": "leave",
	        "flowname": "请假条",
	        "modeid": "1",
	        "nextcheck": [
	            {
	                "name": "貂蝉",
	                "nameid": "3"
	            }
	        ],
	        "mid": "51",
	        "table": "kq_info",
	        "coursers": {
	            "inputid": "0",
	            "name": "主管审核",
	            "id": "1",
	            "num": null,
	            "type": "0"
	        },
	        "courseid": "1",
	        "inputid": "0",
	        "inputrs": [],
	        "isflow": "1",
	        "ncourseid": "2",
	        "fields": {
	            "qjkind": "请假类型",
	            "stime": "开始时间",
	            "etime": "截止时间",
	            "totals": "请假(小时)",
	            "explain": "说明"
	        },
	        "file": [],//相关文件
	        "content": ""
	    },
	    "sysd": {
	        "time": 1471332498,
	        "now": "2016-08-16 15:28:18"
	    }
	}
####<span id="7.1.3">删除单据</span>
	url:HOST/index.php?d=taskrun&m=flow|appapi&a=flowdel&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 格式 1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|mid|是|单据id int|
	|modenum|是|单据类型 在单据详细信息中  flownum|
	|sm|是|删除原因说明|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=flow|appapi&a=flowdel&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&mid=18&modenum=docdeil&sm='写错了'&timekey=1468824191
	返回成示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": "已完成不允许删除",
		    "sysd": {
		        "time": 1468378994,
		        "now": "2016-07-13 11:03:14"
		    }
		}
####<span id="7.1.4">处理单据</span>
	url：HOST/index.php?d=taskrun&m=flow|appapi&a=check&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 格式 1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|flownum|是|单据类型|
	|id|是|单据id|
	|zt|是|处理完单据的状态 1--通过 2--不通过
	|sm|是|不通过时 必填 不通过原因|
	提交示例：
	http://www.ycoa.com/index.php?d=taskrun&m=flow|appapi&a=check&ajaxbool=true&timekey=1471336150&cfrom=appandroid&adminid=4&token=settpdr0&appapikey=69463dfc59bfeb16aa082382b81fe02f&flownum=leave&id=51&zt=2&sm='hhhhh'
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": "处理成功",
	    "sysd": {
	        "time": 1468553071,
	        "now": "2016-07-15 11:24:31"
	    }
	}
###今日会议
	url:HOST/index.php?d=taskrun&m=meet|appapi&a=getmeet&ajaxbool=true
	提交方式 get
	参数说明
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳 格式 int 1458027682|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=meet|appapi&a=getmeet&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468823650
	返回成功示例
	{
    "code":200,
    "msg":"",
    "data":[
        {
            "hytitle":"[今日]2016-08-17(周三)",//会议ri
            "hycontent":[
                {
                    "type":"会议",
                    "hyname":"会议室1",//会议室名
                    "title":"[会议室1]每天部门工作汇报",
                    "titles":"每天部门工作汇报",//会议标题
                    "joinname":"开发部",//参会人
                    "state":"正常</font>",//状态
                    "status":"0",
                    "startdt":"09:30:00至10:30:00",//时间
                    "starttime":1471397400,
                    "endtime":1471401000
                },
                {
                    "type":"会议",
                    "hyname":"会议室2",
                    "title":"[会议室2]这么o",
                    "titles":"这么o",
                    "joinname":"RockOA开发团队,管理部,行政人事,开发部,商务部,财务部,业务部",
                    "state":"正常</font>",
                    "status":"0",
                    "startdt":"16:00:00至16:30:00",
                    "starttime":1471420800,
                    "endtime":1471422600
                },
            ]
        },
    ],
    "sysd":{
        "time":1471415989,
        "now":"2016-08-17 14:39:49"
    }
}
###考勤中心##
####定位打卡
	url:HOST/index.php?d=taskrun&m=kaoqin|appapi&a=dwdk&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 格式1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|location_x|是|纬度 |
	|location_y|是|经度 |
	|scale|是|缩放比例|
	|label|是|标注|
	提交示例：
		http://tryworld.cn/index.php?d=taskrun&m=kaoqin|appapi&a=dwdk&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&location_x=111.1&location_y=111.1&token=r8dwdunf&cfrom=appandroid&scale=0.5&label=1&timekey=1468823678
	返回成功示例
	{
	    "code":"200",
	    "msg":"",
	    "data":"",
	    "sysd":{
	        "time":"1457506711",
	        "now":"2016-03-09 14:58:31"
	    }
	}
####历史定位
	url:HOST/index.php?d=taskrun&m=kaoqin|appapi&a=getlocation&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳 格式  1458027682|
	|appapikey|是|登录成功返回的|
	提交示例：http://tryworld.cn/index.php?d=taskrun&m=kaoqin|appapi&a=getlocation&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468823776

	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": [
	        {
	            "id": "11",
	            "user": "admin",
	            "optdt": "2016-07-12 17:34:35",
	            "uid": "1",
	            "location_y": "111.1",
	            "location_x": "111.1",
	            "scale": "0.5",
	            "label": "1"
	        },
	        {
	            "id": "10",
	            "user": "admin",
	            "optdt": "2016-03-16 15:46:10",
	            "uid": "1",
	            "location_y": "11.1",
	            "location_x": "11.1",
	            "scale": "0",
	            "label": "0"
	        },
	        {
	            "id": "9",
	            "user": "admin",
	            "optdt": "2016-03-16 15:45:51",
	            "uid": "1",
	            "location_y": "11.1",
	            "location_x": "11.1",
	            "scale": "0",
	            "label": "0"
	        },
	        {
	            "id": "8",
	            "user": "admin",
	            "optdt": "2016-03-14 08:28:45",
	            "uid": "1",
	            "location_y": "11.1",
	            "location_x": "11.1",
	            "scale": "0",
	            "label": "0"
	        }
	    ],
	    "sysd": {
	        "time": 1468568656,
	        "now": "2016-07-15 15:44:16"
	    }
	}
####考勤统计
	url:HOST/index.php?d=taskrun&m=kaoqin|appapi&a=getdkjl&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳 格式  1458027682|
	|appapikey|是|登录成功返回的|
	|month|否|格式 2016-03 默认是本月的考勤统计|
	提交示例：http://tryworld.cn/index.php?d=taskrun&m=kaoqin|appapi&a=getdkjl&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&month=2016-03&timekey=1468823829
	返回成功示例：
	{
	    "code":"200",
	    "msg":"",
	    "data":{
	        "18":[
	            "21:25:32" 本月18号 21：25：32打卡
	        ],
	        "26":[
	            "18:49:01",
	            "18:50:05",
	            "18:53:36",
	            "19:26:52",
	            "19:28:57",
	            "19:39:37"
	        ]
	    },
	    "sysd":{
	        "time":"1457507347",
	        "now":"2016-03-09 15:09:07"
	    }
	}
####考勤分析
	url:HOST/index.php?d=taskrun&m=kaoqin|appapi&a=getanay&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳 格式|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|month|否|格式 2016-03 默认是本月的考勤分析|
	提交示例：
		http://HOST/index.php?d=taskrun&m=kaoqin|appapi&a=getanay&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&timekey=1458027682
	返回成功示例：
	{
	    "code": "200",
	    "msg": "",
	    "data": { 
	        "1": { 1号 打卡情况
	            "str": "上班:迟到122分钟(11:02:11)下班:早退263分钟(13:36:51)",
	            "iswork": "1"
	        },
	        "2": { 2号 打卡情况
	            "str": "上班:未打卡</font>下班:早退122分钟(15:57:36)</font>",
	            "iswork": "1"
	        },
        	"3": {
            	"str": "",
            	"iswork": "0"
       		},
        	"99": {  统计打卡情况
	            "迟到": "2",
	            "早退": "2",
	            "未打卡": "14"
        }
    	},
    	"sysd": {
	        "time": "1457508324",
	        "now": "2016-03-09 15:25:24"
    	}
	}
###站内提醒
####站内提醒列表
	url:http://HOST/index.php?d=taskrun&m=index|appapi&a=todo&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳 格式 1458027682|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=index|appapi&a=todo&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468823993
	返回成功示例：	
		{
		    "code": 200,
		    "msg": "",
		    "data": [
		        {
		            "title": "工作任务",
		            "mess": "[管理员]分配一条[研究]工作任务:测试 站内提醒",
		            "status": "1",//状态0 为未读  1为已读
		            "optdt": "2016-07-13 09:42:36",
		            "id": "19",
		            "table": "work",
		            "mid": "16"
		        },
		        {
		            "title": "加班单",
		            "mess": "您提交的[加班单,单号:KJ-20160423-0001]已全部处理完成",
		            "status": "1",
		            "optdt": "2016-04-27 21:47:24",
		            "id": "1",
		            "table": "kq_info",
		            "mid": "57"
		        }
		    ],
		    "sysd": {
		        "time": 1468374223,
		        "now": "2016-07-13 09:43:43"
		    }
		}
####站内提醒详情

[与单据待办详情相同](#7.1.2)
###通知公告
####<span id="7.5.1">通知公告列表</span>
	url:HOST/index.php?d=taskrun&m=gong|appapi&a=getinfor&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳 格式 int 1458027682|
	|stype|否|默认为0 可传参数 0/1 0代表全部 1代表未读|
	提交示例：
		http://tryworld.cn/index.php?d=taskrun&m=gong|appapi&a=getinfor&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468824044
	返回成功示例：
		{
		    "code": "200",
		    "msg": "",
		    "data": {
		        "rows": [
		            {
		                "id": "8",
		                "typename": "技术考核",公告类型
		                "title": "当月2016-03技术KPI考核",标题
		                "optdt": "2016-02-27 11:32:50",创建时间
		                "wd": "1" 未读
		            },
		            {
		                "id": "14",
		                "typename": "通知公告",
		                "title": "欢迎RockOA最新版本V2.2.7版本上线",
		                "optdt": "2016-02-26 21:58:24",
		                "wd": "0" 已读
		            },
          
        		],
        	"wdshu": "1" 未读总数
    	},
    	"sysd": {
        	"time": "1457512047",
        	"now": "2016-03-09 16:27:27"
    	}
	}
####通知公告详情
	url:HOST/index.php?d=taskrun&m=gong|appapi&a=viewinfor&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳 格式 1458027682|
	|appapikey|是|登录成功返回的|
	|id|是|提醒id int|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=gong|appapi&a=viewinfor&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&id=24&cfrom=appandroid&timekey=1468824063
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "id": "14",
	        "num": null,//编号
	        "title": "欢迎RockOA最新版本V2.3.1版本上线",//标题
	        "typenum": "notice",//类型编号
	        "typename": "通知公告",//类型名称
	        "content": "\n\t版本更新了很多内容\n</p>\\n\t1、添加了可自定义模块元素，录入元素。\n</p>\n\n\t2、无需写任何代码即可开发一个流程模块出来喽，详情</a> \n</p>\n\n\t \n</p>",//内容
	        "hits": "23",
	        "enddt": null,//开始时间
	        "startdt": null,//截止时间
	        "optid": "1",
	        "optname": "管理员",//创建人
	        "istt": "0",
	        "xu": "0",
	        "color": null,
	        "isshow": "1",
	        "optdt": "2016-05-08 10:19:52",
	        "zuozhe": "RockOA开发团队",//作者
	        "indate": "2016-05-08",//时间
	        "faobjid": "all",
	        "faobjname": "全体人员",//发布给谁
	        "atype": "0",
	        "isturn": "1",
	        "status": "1"
	    },
	    "sysd": {
	        "time": 1468376180,
	        "now": "2016-07-13 10:16:20"
	    }
	}	
###单据查看
####单据查看列表
	单据查看共分为五类单据，分别是 我的申请、经我处理、我下属申请、未通过、待处理	
	url:http://HOST/index.php?d=taskrun&m=flow|appapi&a=listcheck&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳 格式  1458027682|
	|appapikey|是|登录成功返回的|
	|page int|否|分页，默认为第一页|
	|atype|否|类型，默认为0 0代表我的申请 1代表经我处理 2代表我下属申请 3代表授权查看 4代表未通过 5代表待处理|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=flow|appapi&a=listcheck&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&atype=1&timekey=1468824083
	返回成功示例：	
		{
		    "code": 200,
		    "msg": "",
		    "data": {
		        "rows": [
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
		                "nstatustext": null,
		                "name": "管理员",
		                "deptname": "开发部",
		                "statustext": "赵子龙审核不通过</font>,待赵子龙处理</font>",
		                "modenum": "finfybx",
		                "summary": "报销金额:15.00"
		            }
		        ],
		        "count": 1,
		        "maxpage": 1,
		        "page": 1
		    },
		    "sysd": {
		        "time": 1457576282,
		        "now": "2016-03-10 10:18:02"
		    }
	}	
####单据查看详情
[与单据待办详情相同](#7.1.2)
####单据处理
[与单据待办处理](#7.1.4)
####单据删除
[与单据待办删除](#7.1.3)
###工作任务
####工作任务列表
	工作任务分为三种类型，分别是  未完成、已完成、全部
	url:http://HOST/index.php?d=taskrun&m=work|appapi&a=getdata&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳 格式 int 1458027682|
	|appapikey|是|登录成功返回的|
	|atype|是|0--未完成分配给我的 1--全部 2--报告给我的 3--我创建的|
	|page|否|页码 int|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=work|appapi&a=getdata&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&atype=0&page=1&timekey=1468824211
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": {
		        "rows": [
		            {
		                "id": "2",
		                "type": "开发", 类型
		                "title": "开发界面", 标题
		                "state": "待执行", 状态
		                "startdt": "2016-03-13 09:12:00", 起始时间
		                "enddt": "2016-03-19 09:13:00", 终止时间
		                "dist": "张飞", 分配到 张飞
		                "grade": "中",  难度
		                "baoname": "管理员", 审核人
		                "bgtime": null,
		                "explain": "赶紧做", 说明
		                "optname": "管理员" 操作人
		            },
		        ],
		        "count": 1, 数量
		        "maxpage": 1, 最大页数
		        "page": 1 第一页
		    },
		    "sysd": {
		        "time": 1457753491,
		        "now": "2016-03-12 11:31:31"
		    }
		}
####工作任务详情
	url:http://HOST/index.php?d=taskrun&m=work|appapi&a=xiang&ajaxbool=true
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|timekey|是| 时间戳  int 1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|
	|mid|是|任务id|
	提交示例：
		http://HOST/index.php?d=taskrun&m=work|appapi&a=xiang&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&timekey=1458027682&mid=2
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": {
		        "id": "2",
		        "title": "开发界面", 标题
		        "type": "开发", 类型
		        "grade": "中", 难度 等级
		        "distid": "2", 分配人员id
		        "dist": "张飞", 分配人员
		        "explain": "赶紧做", 说明
		        "baoname": "管理员", 审核人员姓名
		        "baoid": "1", 审核人员id
		        "bgtime": null,报告时间
		        "optdt": "2016-03-11 09:38:26", 操作时间
		        "optid": "1",
		        "optname": "管理员",  操作人姓名
		        "plcont": null,完成时间
		        "status": "1", 状态
		        "startdt": "2016-03-13 09:12:00", 起始时间
		        "enddt": "2016-03-19 09:13:00", 终止时间
		        "wcsj": "0",
		        "wclx": null,
		        "wctime": null,
		        "mid": "0",
		        "dt": null,
		        "state": "待执行", 状态
		        "istx": "1",
		        "projectid": "1",所属项目
		        "zt": "待执行",
		        "logarr": [],
		        "isbg": 0
		    },
		    "sysd": {
		        "time": 1457755138,
		        "now": "2016-03-12 11:58:58"
		    }
		}
####发送工作任务报告
	url：http://HOST/index.php?d=taskrun&m=work|appapi&a=xiang&ajaxbool=true
	提交方式：get，post
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|timekey|是| 时间戳  1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|mid|是|任务id|post|
	|state|是|完成状态|post|
	|explain|是|说明|post|
	提交示例：
	http://HOST/index.php?d=taskrun&m=work|appapi&a=xiang&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&timekey=1458027682&mid=2
		{
		    "mid": "25",
		    "state": "执行中99%",
		    "explain": "尽力了...."
		}
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": "保存成功",
		    "sysd": {
		        "time": 1468824354,
		        "now": "2016-07-18 14:45:54"
		    }
		}
###单据申请
	单据申请分为加班单、请假条、外出出差、会议预定、通知公告、工作日报、工作任务、内部邮件

	如有文件上传，提交分为三步，①利用文件上传接口上传文件返回success②利用获取文件信息接口获取文件的信息③将文件信息的 id与其余信息一同上传。
####单据申请列表
	url:http://HOST/index.php?d=taskrun&m=flow|appapi&a=flowmodelist&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳 格式 1458027682|
	|appapikey|是|登录成功返回的|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=flow|appapi&a=flowmodelist&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=7&token=rw7kf7zq&cfrom=appandroid&timekey=1468823900
	返回成功示例：
	{
		"code": 200,
		 "msg": "",
		    "data": [
		        {
		            "num": "leave",
		            "name": "请假条",
		            "type": "人事考勤",
		            "sort": "0"
		        },
		        {
		            "num": "jiaban",
		            "name": "加班单",
		            "type": "人事考勤",
		            "sort": "1"
		        },
		        {
		            "num": "waichu",
		            "name": "外出出差",
		            "type": "人事考勤",
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
		        },
		        {
		            "num": "daily",
		            "name": "工作日报",
		            "type": "协同办公",
		            "sort": "21"
		        },
		        {
		            "num": "work",
		            "name": "工作任务",
		            "type": "协同办公",
		            "sort": "23"
		        },
		        {
		            "num": "emailin",
		            "name": "内部邮件",
		            "type": "协同办公",
		            "sort": "25"
		        }
		    ],
		    "sysd": {
		        "time": 1468373733,
		        "now": "2016-07-13 09:35:33"
		    }
		}
####加班单
#####提交加班单
	url:http://HOST/index.php?d=taskrun&m=flow_jiaban|appapi&a=save&ajaxbool=true
	提交方式：get post
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|timekey|是| 时间戳   1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|stime|是|开始时间 格式为 2016-03-10 16:01:00|post|
	|etime|是|结束时间 格式为 2016-03-10 16:01:00|	post|
	|totals|是|总时长(int 类型)|post|
	|explain|是|说明|post|
	提交示例：
		http://tryworld.cn/index.php?d=taskrun&m=flow_jiaban|appapi&a=save&ajaxbool=true&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468824830
		post数据：
			{
			    "stime": "2016-03-14 11:01:01",
			    "etime": "2016-03-15 8:00:00",
			    "totals": "24",
			    "explain": "加班"
			}
	返回成功示例：
	{
		"code": 200,
		 "msg": "",
		 "data": "提交成功",
		 "sysd": {
		  	"time": 1457594840,
		    "now": "2016-03-10 15:27:20"
	 		}
	}
#####获取加班单时间差
	url:http://HOST/index.php?d=taskrun&m=flow_jiaban|appapi&a=total&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|timekey|是| 时间戳   1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|stime|是| 开始时间格式为 2016-07-15 12:00:00|get|
	|etime|是| 结束时间格式为 2016-07-16 12:00:00|get|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=flow_jiaban|appapi&a=total&ajaxbool=true&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468824895&stime=2016-07-18+14%3A54%3A55&etime=2016-07-16+12%3A00%3A00
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": 24,
	    "sysd": {
	        "time": 1468555171,
	        "now": "2016-07-15 11:59:31"
	    }
	}
####请假条
#####提交请假条
	url:http://HOST/index.php?d=taskrun&m=flow_leave|appapi&a=save&ajaxbool=true
	提交方式：get post
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|timekey|是| 时间戳   1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|qjkind|是|请假类型分为 事假、病假、年假、婚假|post|
	|stime|是|开始时间 格式为 2016-03-10 16:01:00|post|
	|etime|是|结束时间 格式为 2016-03-10 16:01:00|	post|
	|totals|是|总时长|post|
	|explain|是|说明|post|
	提交示例：
		http://HOST/index.php?d=taskrun&m=flow_leave|appapi&a=save&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&timekey=1458027682
		post数据：
			{
			    "qjkind": "病假",
			    "stime": "2016-03-14 11:01:01",
			    "etime": "2016-03-15 8:00:00",
			    "totals": "24小时",
			    "explain": "有病"
			}
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": "提交成功",
		    "sysd": {
		        "time": 1457594840,
		        "now": "2016-03-10 15:27:20"
		    }
		}
#####获取请假时间差
	url:http://HOST/index.php?d=taskrun&m=flow_leave|appapi&a=totalweb&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|timekey|是| 时间戳   1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|stime|是|开始时间 格式为 2016-03-10 16:01:00|post|
	|etime|是|结束时间 格式为 2016-03-10 16:01:00|	post|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=flow_leave|appapi&a=totalweb&ajaxbool=true&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468825053&stime=2016-07-15+12%3A00%3A00&etime=2016-07-16+12%3A00%3A00
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": 8,
	    "sysd": {
	        "time": 1468565269,
	        "now": "2016-07-15 14:47:49"
	    }
	}
####外出出差
	url:http://HOST/index.php?d=taskrun&m=flow_waichu|appapi&a=save&ajaxbool=true
	提交方式：get post
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|timekey|是| 时间戳 1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|atype|是|外出类型 选项为 外出、出差|post|
	|outtime|是|外出时间 格式为 2016-03-10 16:01:00|	post|
	|intime|是|预计回岗 格式为 2016-03-10 16:01:00|post|
	|address|是|外出地址|post|
	|reason|是|外出事由|post|
	|explain|否|说明|post
	提交示例：
		http://HOST/index.php?d=taskrun&m=flow_waichu|appapi&a=save&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&timekey=1458027682
		post数据：
			{
				"atype": "外出",
			    "outtime": "2016-03-14 11:01:01",
			    "intime": "2016-03-15 8:00:00",
			    "address": "唐山",
			    "reason": "外出"
			}
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": "提交成功",
		    "sysd": {
		        "time": 1457594840,
		        "now": "2016-03-10 15:27:20"
		    }
		}
####会议预定
#####获取会议室
	url:HOST/index.php?d=taskrun&m=meet|appapi&a=getcans&ajaxbool=true
	提交方式：get
	参数说明:
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|timekey|是| 时间戳 1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=meet|appapi&a=getcans&ajaxbool=true&adminid=1&token=g128m5gi&cfrom=appandroid&appapikey=69463dfc59bfeb16aa082382b81fe02f&timekey=1471337619
	返回示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "hyname": [
	            {
	                "name": "会议室1"
	            }
	        ]
	    },
	    "sysd": {
	        "time": 1468394795,
	        "now": "2016-07-13 15:26:35"
	    }
	}
#####会议室预定
	url:http://HOST/index.php?d=taskrun&m=meet|appapi&a=save&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|timekey|是| 时间戳 1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|hyname|是|会议室名 如：会议室1|get|
	|title|是|会议主题|get|
	|startdt|是|会议开始时间 格式为2016-07-14 11：00：00|get|
	|enddt|是|会议结束时间 格式为2016-07-14 11：00：00 |get|
	|istz|否|是否 到时提醒 0表示不提醒 1表示提醒  int|get|
	|joinname|否|示例：行政人事,管理员,商务部|get|
	|joinid|否|示例：d3,u1,d5|get|
	|explain|否|s说明|get|
	注：joinid中： d3表示部门id为3的人，u2表示用户id为2的 人
	
	提交示例：
		http://www.ycoa.com/index.php?d=taskrun&m=meet|appapi&a=save&ajaxbool=true&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468825518&hyname='会议室1'&title='这是测试会议'&startdt='2016-07-1514:00:00'&enddt='2016-07-1517:00:00'&istz=0&joinname='行政人事,管理员,商务部'&joinid=d3,u1,d5
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": "提交成功",
		    "sysd": {
		        "time": 1468398046,
		        "now": "2016-07-13 16:20:45"
		    }
		}
####<span id="7.8.5">信息公告</span>
#####获取信息公告分类列表
	url：   HOST?d=taskrun&m=gong|appapi&a=getInfo&ajaxbool=true
	提交方式：get 
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|timekey|是| 时间戳 1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	提交示例：
	http://www.ycoa.com/index.php?d=taskrun&m=gong|appapi&a=getInfo&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=4&token=8lx8cizt&cfrom=appandroid&timekey=1471654777
	返回成功示例：
	{
	    "code":200,
	    "msg":"",
	    "data":[
	        {
	            "name":"通知公告",
	            "num":"notice"
	        },
	        {
	            "name":"规章制度",
	            "num":"rules"
	        },
	        {
	            "name":"企业文化",
	            "num":"culture"
	        },
	        {
	            "name":"奖惩通告",
	            "num":"jiang"
	        }
	    ],
	    "sysd":{
	        "time":1471653769,
	        "now":"2016-08-20 08:42:49"
	    }
	}
#####提交信息公告
	url:http://HOST/index.php?d=taskrun&m=gong|appapi&a=savegong&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|timekey|是| 时间戳 1458027682|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|title|是|公告主题|get|
	|typenum|是|值为 分类列表的中  num|get|
	|typename|是|值 为 分类列表中的 name |get
	|content|是|公告内容|get|
	|zuozhe|否|发布者/部门|get|
	|faobjname|否|发布给 示例：行政人事,管理员,商务部|get|
	|faobjid|否|示例：d7,u4,u1|get|
	注：joinid中： d3表示部门id为3的人，u2表示用户id为2de 人
	提交示例：
	http://www.ycoa.com/index.php?d=taskrun&m=gong|appapi&a=savegong&ajaxbool=true&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=4&token=8lx8cizt&cfrom=appandroid&timekey=1471656379&title='app公告'&content='app公告'&typenum=jiang&typename=奖惩通告
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": "提交成功",
	    "sysd": {
	        "time": 1468401647,
	        "now": "2016-07-13 17:20:47"
	    }
	}
####工作日报
	url:http://HOST/index.php?d=taskrun&m=flow_daily|appapi&a=saveweb&ajaxbool=true
	提交方式：get post
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳  1458027682|get|
	|dts|否| -1为昨天 0或者默认为今天 -2为前天|get|
	|content|是|内容|get|
	|plan|否|下次计划|get|
	|fileid|否|文件信息id|get|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=flow_daily|appapi&a=saveweb&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&dts=-1&content='app日报'&plan='app日报'&timekey=1468825883
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": "success",
	    "sysd": {
	        "time": 1468456479,
	        "now": "2016-07-14 08:34:39"
	    }
	}
####工作任务####
#####获取工作任务的基本信息
	url:http://HOST/index.php?d=taskrun&m=work|appapi&a=getcans&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|appapikey|是|登录成功返回的|
	|timekey|是| 时间戳  1458027682|get|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=work|appapi&a=getcans&ajaxbool=true&adminid=1&token=g128m5gi&cfrom=appandroid&appapikey=69463dfc59bfeb16aa082382b81fe02f&timekey=1471337723
	返回成功示例：
	{
    "code": 200,
    "msg": "",
    "data": {
        "type": [//任务类型
            {
                "name": "设计"
            },
            {
                "name": "开发"
            },
            {
                "name": "测试"
            },
            {
                "name": "研究"
            },
            {
                "name": "讨论"
            },
            {
                "name": "改进"
            },
            {
                "name": "bug"
            },
            {
                "name": "其它"
            }
        ],
        "grade": [//任务等级
            {
                "name": "低"
            },
            {
                "name": "中"
            },
            {
                "name": "高"
            },
            {
                "name": "紧急"
            }
        ],
        "project": [//项目
            {
                "id": "1",
                "name": "开发App(执行中0%)"
            }
        ]
		},
		    "sysd": {
		        "time": 1468457298,
		        "now": "2016-07-14 08:48:18"
		    }
		}
#####发布工作任务
	url:http://HOST/index.php?d=taskrun&m=work|appapi&a=savework&ajaxbool=true
	提交方式：get
	参数说明：
|参数名|是否必须|说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	|title|是|任务标题|get|
	|type|是|任务分类 如：设计 字符串类型|get|
	|grade|是|任务等级 如：低|get|
	|dist|是|分配给  的 名称|get|
	|distid|是|分配给的id 以‘，’分隔|get|
	|startdt|是|开始时间 格式是 2016-07-14 08:54：11|get|
	|enddt|否|截止时间|get|
	|explain|否|任务说明|get|
	|baoname|否|示例：行政人事,管理员,商务部|get|
	|baoid|否|示例：d3,u1,d5|get|
	|explain|否|s说明|get|
	|projectid|否|项目id|get|
	|fileid|否|文件信息id|get|
	
	注：baoid中： d3表示部门id为3的人，u2表示用户id为2de 人	
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=work|appapi&a=savework&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&title=appwork&type=设计&grade=高&dist=张飞&distid=8&startdt=2016:07:18&timekey=1468825935
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": null,
	    "sysd": {
	        "time": 1468459744,
	        "now": "2016-07-14 09:29:04"
	    }
	}	

####内部邮件
	暂无
##通讯录
###<span id="8.1">组织结构</span>
	url:HOST/index.php?d=taskrun&m=user|appapi&a=getdeptadmin&ajaxbool=true
	提交方式：get
	参数说明：
|参数名|是否必须|说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=user|appapi&a=getdeptadmin&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468826030
	返回成功示例：
	{
    "code":200,
    "msg":"",
    "data":[
        {
            "children":[
                {
                    "children":[
                        {
                            "id":"u7",//用户代码  用于选择人员时 使用
                            "name":"刘备",//用户名
                            "gender":"男",//性别
                            "ranking":"董事长",//职位
                            "deptname":"管理部",//部门
                            "face":"images/im/user1.jpg",//头像
                            "imonline":"0",//是否在线
                            "leaf":true,
                            "uid":"7",//用户id  
                            "type":"u",//类型 u-用户 d-部门 c-公司
                            "icon":"mode/icons/user.png"
                        }
                    ],
                    "name":"管理部",
                    "id":"d7",
                    "did":"7",
                    "type":"d"
                },
            ],
            "name":"永昌物流",
            "id":"d1",
            "did":"1",
            "type":"d"
        },
    ],
    "sysd":{
        "time":1471832294,
        "now":"2016-08-22 10:18:14"
    }
}
###群/讨论组
####获取群组列表
	url:HOST/index.php?d=taskrun&m=index|appapi&a=getgroup&ajaxbool=true
	提交方式：get
	参数说明：
|参数名|是否必须|说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=index|appapi&a=getgroup&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468826063
	返回成功示例：
	type:0为 群  1为讨论组  2为应用信息
	{
	    "code":200,
	    "msg":"",
	    "data":[
	        {
	            "type":"0",
	            "name":"技术群",//群组名称
	            "id":"1",//群组id
	            "face":"images/group.png",//群组 图标
	            "sort":"0"
	        },
	        {
	            "type":"2",
	            "name":"通知公告",
	            "id":"3",
	            "face":"webreim/client/images/im/laba.png",
	            "sort":"0"
	        },
	        {
	            "type":"2",
	            "name":"会议通知",
	            "id":"4",
	            "face":"webreim/client/images/im/meet.png",
	            "sort":"0"
	        },
	        {
	            "type":"2",
	            "name":"单据待办",
	            "id":"7",
	            "face":"webreim/client/images/im/daibans.png",
	            "sort":"0"
	        },
	        {
	            "type":"1",
	            "name":"哈哈哈",
	            "id":"8",
	            "face":"images/taolun.png",
	            "sort":"0"
	        },
	        {
	            "type":"1",
	            "name":"OA项目讨论",
	            "id":"9",
	            "face":"images/taolun.png",
	            "sort":"0"
	        },
	        {
	            "type":"2",
	            "name":"项目任务",
	            "id":"12",
	            "face":"webreim/client/images/im/renwu.png",
	            "sort":"8"
	        },
	        {
	            "type":"2",
	            "name":"万年历",
	            "id":"13",
	            "face":"images/calendar.png",
	            "sort":"10"
	        }
	    ],
	    "sysd":{
	        "time":1471220592,
	        "now":"2016-08-15 08:23:11"
	    }
	}
#####同步群组信息#####
	在点击 群组名称 后可以触发
	
	url:http://HOST/index.php?d=teskrun&m=reim|appapi&a=getgroupreinfo&ajaxbool=true
	提交方式：get
	参数说明：
|参数名|是否必须|说明|
	|-----|:-----|----|
	|adminid|是|用户id|
	|token|是|用户登录成功后返回的token|
	|cfrom|是|appandroid(安卓)，appiphone(ios)，clien(客户端）|
	|timekey|是| 时间戳  1458027682|get|
	|receid|是|群组id|
	|type|是|group|
	|loadcount|否|默认为1 为1返回群组人员信息 不为1则不返回群组人员|
	|appapikey|是|登录成功返回的|get|
	提交示例：
	http://www.ycoa.com/index.php?d=taskrun&m=reim|appapi&a=getgroupreinfo&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1471223708&loadcount=2&type=group&receid=8	
	返回成功示例：
	说明：默认返回10条未读信息，wdtotal为剩余未读总数 可以再次调用本接口 获取未读消息
	（类似于qq上拉获取消息）
	{
	    "code":200,
	    "msg":"",
	    "data":{
	        "rows":[
	            {
	                "optdt":"2016-08-12 16:40:16",//信息发送时间
	                "zt":"1",//信息状态 1 代表已读  0代表未读
	                "id":"146",/信息id
	                "cont":"app测试",//信息内容
	                "sendid":"7",//发送者id
	                "table":null,
	                "mid":null,
	                "face":"images/noface.png",//发送者头像
	                "sendname":"刘备"//发送者名字
	            },
	            
	        ],
	        "wdtotal":0//剩余未读总数
	    },
	    "sysd":{
	        "time":1471223708,
	        "now":"2016-08-15 09:15:08"
	    }
	}	
#####发送群组信息#####
	url：http://HOST/index.php?d=taskrun&m=reim|appapi&a=sendgroup&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
		|-----|:------:|----|
		|adminid|是| 用户id int|get|
		|token|是| 用户登录成功后返回的token |get|
		|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
		|timekey|是| 时间戳  1458027682|get|
		|appapikey|是|登录成功返回的|get|
		|receid|是|群组id int|get|
		|cont|是|信息内容|get|
		|optdt|是|时间 格式为 2016-3-11 10：01：00|get|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=reim|appapi&a=sendgroup&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&receid=8&cont=app测试&timekey=1468826131	
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": {
		        "cont": "app测试",//内容
		        "sendid": 1,//发送方
		        "receid": "4,7,9,10,8,3,5",//接收方
		        "receuid": "1,4,7,9,10,8,3,5",//群组的人员
		        "type": "group",//发送类型
		        "optdt": "2016-",//发送时间
		        "zt": "1",
		        "id": 8,
		        "nuid": "",
		        "gid": "8"
		    },
		    "sysd": {
		        "time": 1468467970,
		        "now": "2016-07-14 11:46:10"
		    }
		}
#####同步个人聊天信息#####
	点击个人聊天后可触发
	url:http://HOST/index.php?d=taskrun&m=reim|appapi&a=getuserreinfo&ajaxbool=true
	提交方式：get
	参数说明：
|参数名|是否必须|说明|
	|-----|:-----:|----|
	|adminid|是|用户id|
	|token|是|用户登录成功后返回的token|
	|cfrom|是|appandroid(安卓)，appiphone(ios)，client(客户端）|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	|receid|是|接收用户id int|
	提交示例：
	http://www.ycoa.com/index.php?d=taskrun&m=reim|appapi&a=getuserreinfo&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1471227259&receid=7
	说明：wdtotal大于0的时候代表有未读消息  等于0的时候返回5条最新的消息
	返回成功示例：
	{
	    "code":200,
	    "msg":"",
	    "data":{
	        "rows":[
	            {
	                "optdt":"2016-08-15 10:08:22",
	                "zt":"1",
	                "id":"169",
	                "cont":"app测试222",
	                "sendid":"7",
	                "table":null,
	                "mid":null,
	                "face":"images/noface.png",
	                "sendname":"刘备"
	            },
	            {
	                "optdt":"2016-08-15 10:08:21",
	                "zt":"1",
	                "id":"168",
	                "cont":"app测试222",
	                "sendid":"7",
	                "table":null,
	                "mid":null,
	                "face":"images/noface.png",
	                "sendname":"刘备"
	            },
	            {
	                "optdt":"2016-08-15 10:08:20",
	                "zt":"1",
	                "id":"167",
	                "cont":"app测试222",
	                "sendid":"7",
	                "table":null,
	                "mid":null,
	                "face":"images/noface.png",
	                "sendname":"刘备"
	            },
	            {
	                "optdt":"2016-08-15 10:08:20",
	                "zt":"1",
	                "id":"166",
	                "cont":"app测试222",
	                "sendid":"7",
	                "table":null,
	                "mid":null,
	                "face":"images/noface.png",
	                "sendname":"刘备"
	            },
	            {
	                "optdt":"2016-08-15 10:08:19",
	                "zt":"1",
	                "id":"165",
	                "cont":"app测试222",
	                "sendid":"7",
	                "table":null,
	                "mid":null,
	                "face":"images/noface.png",
	                "sendname":"刘备"
	            }
	        ],
	        "wdtotal":0
	    },
	    "sysd":{
	        "time":1471227287,
	        "now":"2016-08-15 10:14:47"
	    }
	}
#####发送信息至个人####
	url:http://HOST/index.php?d=taskrun&m=reim|appapi&a=sendgroup&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	|receid|是|接收用户id int|
	|cont|是|信息内容|
	|optdt|是|时间 格式为 2016-3-11 10：01：00|
	提交示例：
	http://tryworld.cn/index.php?d=taskrun&m=reim|appapi&a=senduser&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=7&receid=1&cont=app测试&optdt=2016-07-18+15%3A16%3A15&token=rw7kf7zq&cfrom=appandroid&timekey=1468826175
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": {
		        "cont": "app测试",
		        "sendid": 1,
		        "receid": "2",
		        "type": "user",
		        "optdt": "2016-07-14 16:31:45",
		        "zt": "0",
		        "ftype": "1",
		        "receuid": "1,2",
		        "id": 10,
		        "nuid": ""
		    },
		    "sysd": {
		        "time": 1468485105,
		        "now": "2016-07-14 16:31:45"
		    }
		}	
#####删除聊天信息#####
	url:http://HOST/index.php?d=taskrun&m=reimjilu|appapi&a=delrecord&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	|ids|是|如批量删除 应用逗号隔开 “,”|get|
	提交示例：
		http://www.ycoa.com/index.php?d=taskrun&m=reimjilu|appapi&a=delrecord&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1471228369&ids=169
	返回成功示例：
	{
	    "code":200,
	    "msg":"",
	    "data":"删除成功",
	    "sysd":{
	        "time":1471228369,
	        "now":"2016-08-15 10:32:49"
	    }
	}

#####查看信息详细内容#####
	url:http://HOST/index.php?d=taskrun&m=reim|appapi&a=getmess&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id int|get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	|messid|是|信息id|get|
	提交示例：
	返回成功示例：
		{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "id": "8",//信息id
	        "optdt": null,
	        "zt": "1",//信息状态
	        "cont": "app测试",//信息内容
	        "sendid": "1",
	        "receid": "8",
	        "receuid": "1,4,7,9,10,8,3,5",
	        "type": "group",
	        "optid": null,
	        "optname": null,
	        "table": null,
	        "mid": null,
	        "url": null,
	        "ftype": "0",
	        "ists": "0",
	        "tstime": null
	    },
	    "sysd": {
	        "time": 1468484363,
	        "now": "2016-07-14 16:19:23"
	    }
	}
#####同步个人信息列表#####
	url:http://HOST/index.php?d=taskrun&m=reim|appapi&a=getwdmesslist&ajaxbool=true
	提交方式:get
	说明：有未读消息的情况下 先读取未读消息，若无则判断maxmessid，若maxmessid=0，则返回当天的聊天记录，若maxmessid>0 则读取id>=maxmessid的聊天记录
	参数说明：
|参数名 | 是否必须 | 说明|
		|-----|:------:|----|
		|adminid|是| 用户id int|
		|token|是| 用户登录成功后返回的token |
		|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
		|timekey|是| 时间戳  1458027682|
		|appapikey|是|登录成功返回的|get|
		|receid|是|发送者用户id|
		|type|是|user|
		|maxmessid|是||
	提交示例：
		http://HOST/index.php?d=taskrun&m=reim|appapi&a=getwdmesslist&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&timekey=1458027682&receid=2&type=user&maxmessid=0
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": [
		        {
		            "id": "770",
		            "optdt": "2016-03-11 10:37:08",
		            "zt": "1",
		            "cont": "哈哈",
		            "sendid": "1",
		            "receid": "2",
		            "receuid": "1,2",
		            "type": "user",
		            "optid": null,
		            "optname": null,
		            "table": null,
		            "mid": null,
		            "url": null,
		            "ftype": "1",
		            "ists": "0",
		            "tstime": null
		        }
		    ],
		    "sysd": {
		        "time": 1457684965,
		        "now": "2016-03-11 16:29:25"
		    }
		}
#####同步群组信息
	url:http://HOST/index.php?d=taskrun&m=reim|appapi&a=getwdgrouplist&ajaxbool=true
	提交方式：get
	说明：有未读消息的情况下 先读取未读消息，若无则判断maxmessid，若maxmessid=0，则返回当天的聊天记录，若maxmessid>0 则读取id>=maxmessid的聊天记录
	参数说明：
|参数名 | 是否必须 | 说明|
		|-----|:------:|----|
		|adminid|是| 用户id int|
		|token|是| 用户登录成功后返回的token |
		|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
		|timekey|是| 时间戳  1458027682|
		|appapikey|是|登录成功返回的|get|
		|receid|是|群组id int|
		|aid|是| 当前登录的用户id int |
		|type|是|group|
		|maxmessid|是||
	提交示例：
		http://HOST/index.php?d=taskrun&m=reim|appapi&a=getwdgrouplist&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&timekey=1458027682&receid=2&type=group&maxmessid=0
	返回成功示例：
		{
		    "code": 200,
		    "msg": "",
		    "data": {
		        "rows": [
		            {
		                "optdt": "2016-03-11 00:00:00",
		                "zt": "1",
		                "id": "775",
		                "cont": "哈哈",
		                "sendid": "1",
		                "table": null,
		                "mid": null,
		                "face": "upload/2015-08/1440578146698_4091.jpg",
		                "sendname": "管理员"
		            }
		        ],
		        "wdtotal": 0
		    },
		    "sysd": {
		        "time": 1457685776,
		        "now": "2016-03-11 16:42:56"
		    }
		}
	
####同步聊天记录####
	url:http://HOST/index.php?d=taskrun&m=reim|appapi&a=getreload&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id int|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|timekey|是| 时间戳  1458027682|
	|appapikey|是|登录成功返回的|get|
	|receid|是|群组id int|
	|aid|是| 当前登录的用户id int |
	|type|是|group|
	|maxmessid|是||
	
	提交示例：
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "rows": [
	            {
	                "optdt": "2016-07-14 17:13:41",
	                "zt": "0",
	                "id": "14",
	                "cont": "app测试",
	                "sendid": "1",
	                "table": null,
	                "mid": null,
	                "face": "http://www.ycoa.com/upload/2015-08/1440578146698_4091.jpg",
	                "sendname": "管理员"
	            },
	            {
	                "optdt": "2016-07-14 17:13:39",
	                "zt": "0",
	                "id": "13",
	                "cont": "app测试",
	                "sendid": "1",
	                "table": null,
	                "mid": null,
	                "face": "http://www.ycoa.com/upload/2015-08/1440578146698_4091.jpg",
	                "sendname": "管理员"
	            },
	            {
	                "optdt": "2016-07-14 17:13:36",
	                "zt": "0",
	                "id": "12",
	                "cont": "app测试",
	                "sendid": "1",
	                "table": null,
	                "mid": null,
	                "face": "http://www.ycoa.com/upload/2015-08/1440578146698_4091.jpg",
	                "sendname": "管理员"
	            },
	            {
	                "optdt": "2016-07-14 17:13:35",
	                "zt": "0",
	                "id": "11",
	                "cont": "app测试",
	                "sendid": "1",
	                "table": null,
	                "mid": null,
	                "face": "http://www.ycoa.com/upload/2015-08/1440578146698_4091.jpg",
	                "sendname": "管理员"
	            },
	            {
	                "optdt": "2016-07-14 16:31:45",
	                "zt": "0",
	                "id": "10",
	                "cont": "app测试",
	                "sendid": "1",
	                "table": null,
	                "mid": null,
	                "face": "http://www.ycoa.com/upload/2015-08/1440578146698_4091.jpg",
	                "sendname": "管理员"
	            }
	        ],
	        "wdtotal": 0
	    },
	    "sysd": {
	        "time": 1468489698,
	        "now": "2016-07-14 17:48:18"
	    }
	}
######获取聊天记录#####
	url:http://HOST/index.php?d=taskrun&m=reimjilu|appapi&a=data&ajax=bool
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id |
	|timekey|是|时间戳 格式  1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|get|
	|sid|是|接收方id|
	|page|是 int|页数|
	返回成功示例：
	{
	    "code":200,
	    "msg":"",
	    "data":{
	        "data":[
	            {
					"id":"25",//信息id
	                "optdt":"2016-07-16 09:27:39",//信息创建时间
	                "zt":"1",//信息id
	                "cont":"app测试",//消息内容
	                "sendid":"7",//发送方id
	                "receid":"1",//接收方id
	                "receuid":"7,1",
	                "type":"user",
	                "optid":null,
	                "optname":null,
	                "table":null,
	                "mid":null,
	                "url":null,
	                "ftype":"1",
	                "ists":"0",
	                "tstime":null,
	                "sendname":"刘备",//发送者姓名
                	"sendface":"images/noface.jpg"//发送方头像
				}
	        ],
	        "count":19,//聊天记路总数
	        "page":1,//第一页
	        "maxpage":1//共一页
	    },
	    "sysd":{
	        "time":1471229376,
	        "now":"2016-08-15 10:49:36"
	    }
	}
###联系人
	url:http://HOST/index.php?d=taskrun&m=user|appapi&a=getuser&ajaxbool=true
	参数说明：
|参数名|是否必须|说明|提交方式|
	|-----|:------:|----|
	|adminid|是| 用户id |get|
	|token|是| 用户登录成功后返回的token |get|
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |get|
	|timekey|是| 时间戳  1458027682|get|
	|appapikey|是|登录成功返回的|get|
	提交方式：get
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": "1|管理员|OA项目经理|开发部|4|upload/2015-08/1440578146698_4091.jpg,2|RockOA客服|工程师|开发部|4|upload/2015-08/24_1510166137.png,7|刘备|董事长|管理部|7|,4|大乔|行政主管|行政人事|3|,3|貂蝉|人事经理|行政人事|3|upload/2015-08/02_2246506417_crop8455.jpg,5|小乔|行政前台|行政人事|3|upload/2015-08/30_1448539797_crop9267.jpg,8|张飞|程序员|开发部|4|,9|赵子龙|财务经理|财务部|6|,10|吕布|出纳|财务部|6|",
	    "sysd": {
	        "time": 1468460210,
	        "now": "2016-07-14 09:36:50"
	    }
	}
	注：10|吕布|出纳|财务部|6| d 10为用户id  吕布为用户名  出纳为职位  财务部为部门名  6为部门id  路径为 头像
##上传文件
###上传文件
	url:http://HOST/index.php?d=taskrun&m=upload|appapi&a=upfile&ajaxbool=true
	提交方式 以文件形式上传  文件的后缀支持为|jpg|png|gif|jpeg|bmp|docx|doc|zip|rar|xls|xlsx|ppt|pptx|pdf|
	参数说明： 
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id |
	|timekey|是|时间戳 格式  1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|get|
	提交成功示例：
	
	返回成功示例：
	{
	    "code":200,
	    "msg":"",
	    "data":"上传文件成功",
	    "sysd":{
	        "time":1471393325,
	        "now":"2016-08-17 08:22:05"
	    }
	}
###获取上传文件信息
	url:HOST/index.php?d=taskrun&m=upload|appapi&a=getfile&ajaxbool=true
	提交方式：get
	参数说明：
|参数名 | 是否必须 | 说明|
	|-----|:------:|----|
	|adminid|是| 用户id |
	|timekey|是|时间戳 格式  1458027682|
	|token|是| 用户登录成功后返回的token |
	|cfrom|是| appandroid(安卓)，appiphone（ios），client（客户端） |
	|appapikey|是|登录成功返回的|get|
	提交成功示例：
		http://tryworld.cn/index.php?d=taskrun&m=upload|appapi&a=getfile&ajaxbool=true&appapikey=69463dfc59bfeb16aa082382b81fe02f&adminid=1&token=r8dwdunf&cfrom=appandroid&timekey=1468826608
	返回成功示例：
	{
	    "code": 200,
	    "msg": "",
	    "data": {
	        "adddt": "2016-07-15 09:55:41",
	        "valid": 1,
	        "filename": "fanyi.docx",
	        "web": "Firefox",
	        "ip": "127.0.0.1",
	        "fileext": "docx",
	        "filesize": 54679,
	        "filesizecn": "53.40 KB",
	        "filepath": "upload/2016-07/15_0955418297.docx",
	        "optid": 1,
	        "optname": "管理员",
	        "id": 12,
	        "thumbpath": "upload/2016-07/15_0955418297.docx",
	        "picw": 0,
	        "pich": 0
	    },
	    "sysd": {
	        "time": 1468547954,
	        "now": "2016-07-15 09:59:14"
	    }
	}