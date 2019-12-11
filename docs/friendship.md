### 好友相关接口

| 接口地址 | 说明 |
|---------|-----|
| [/friendship/invite](#post-friendshipinvite) | 发起添加好友 |
| [/friendship/agree](#post-friendshipagree) | 同意加好友请求 |
| [/friendship/ignore](#post-friendshipignore) | 忽略好友请求 |
| [/friendship/delete](#post-friendshipdelete) | 删除好友请求 |
| [/friendship/setDisplayName](#post-setDisplayName) | 设置好友备注名 |
| [/friendship/all](#get-friendshipall) | 获取好友列表 |
| [/friendship/getContactsInfo](#post-getContactsInfo) | 获取通讯录朋友信息列表 |
## API 说明

### RestFul /friendship/invite/{friendID}/{message}/{source}

添加好友

#### 请求示列

```
/friendship/invite/5/你好， 我叫xxx/来自账号搜索

```

* friendID : 好友ID
* message : 请求加好友描述
* source : 来源

#### 返回结果

正常返回，返回的 HTTP Status Code 为 200，返回的内容如下：

```
{
    code: 200,
    message: "已发送好友请求"
}
```
 
返回码说明：

* 200: 请求成功
* 2000: {friendID}就是自己，所以无法发起请求
* 2001: 未查到ID为{friendID}的用户
* 2002: 已是好友
* 2003: 后台添加数据失败


### RestFul /friendship/agree/{friendID}

同意好友请求

#### 请求示列

```

/friendship/agree/6

```

* friendID: 好友 Id

#### 返回结果

正常返回，返回的 HTTP Status Code 为 200，返回的内容如下：

```
{
    code: 200,
    message: "已同意"
}
``` 

返回码说明：

* 200: 请求成功
* 2004: 对方未邀请您

### RestFul /ignore/{friendID}

忽略好友请求

#### 请求示列

```
/ignore/5

```

* friendID:  好友 Id

#### 返回结果

正常返回，返回的 HTTP Status Code 为 200，返回的内容如下：

```
{
    code: 200,
    message: "已忽略"
}
``` 

返回码说明：

* 200: 请求成功
* 2005: 对方未邀请您

### RestFul /delete/{friendID}

删除好友

#### 请求示列

```
/delete/5

```

* friendID: 好友 Id

#### 返回结果

正常返回，返回的 HTTP Status Code 为 200，返回的内容如下：

```
{
    code: 200,
    message: "已删除"
}
``` 

返回码说明：

* 200: 请求成功
* 2006: 对方不是您的好友

### RestFul /setDisplayName/{friendID}/{displayName}

设置好友备注名称

#### 请求示列

```
/setDisplayName/5/小黑

```

* friendID: 好友 Id
* displayName: 备注

#### 返回结果

正常返回，返回的 HTTP Status Code 为 200，返回的内容如下：

```
{
    code: 200,
    message: "已更改备注"
}
``` 

返回码说明：

* 200: 请求成功 
* 2007: 备注名称超限
* 2008: 对方不是您的好友

### RestFul /friendship/all

获取好友关系列表

#### 请求示列

```
/friendship/all
```

#### 返回结果

正常返回，返回的 HTTP Status Code 为 200，返回的内容如下：

```
{

    code: 200,
    message: "OK",
    result: [
    		{
    		    id: 25,
    		    source: "来自账号搜索",
    		    message: "你好， 我叫xxx",
    		    status: "20",
    		    statusUpdateTime: "1576043769821",
    		    friendId: 5,
    		    displayName: "小花",
    		    nickname: "kxr111",
    		    portraitUri: "http://www.sucaijishi.com/uploadfile/2016/0203/20160203022630582.png",
    		    gender: "male",
    		    phone: "131"
    		},
    		{
    		    id: 27,
    		    source: "来aah",
    		    message: "你好，我是kxr111",
    		    status: "11",
    		    statusUpdateTime: "1576046682578",
    		    friendId: 7,
    		    displayName: null,
    		    nickname: "kxr113",
    		    portraitUri: "http://www.sucaijishi.com/uploadfile/2016/0203/20160203022630582.png",
    		    gender: "male",
    		    phone: "121"
    		}
    ]
}

```
* id: 好友关系ID
* source: 来源， 比如扫描、搜索账号、明信片推荐等
* displayName: 好友备注
* message: 请求加好友描述
* status: 好友关系状态 10: 请求, 11: 被请求, 20: 同意, 21: 忽略, 30: 被删除
* statusUpdateTime: 最后一次好友状态修改时间 
* friendId: 对方ID
* nickname: 对方昵称
* gender: 性别
* phone: 手机号
* portraitUri: 头像

返回码说明：

* 200: 请求成功


### RestFul /getContactsInfo/{contacstList}

 
#### 请求示列
```
friendship/getContactsInfo/13180273322,15177362245,13588376462
```
#### 返回结果

正常返回，返回的 HTTP Status Code 为 200，返回的内容如下：

```
{
    code: 200,
    message: "OK",
    result: [
        {
        relationship: 1,
        userid: 5,
        stAccount: "kxr111",
        nickname: "kxr111",
        portraitUri: "http://www.sucaijishi.com/uploadfile/2016/0203/20160203022630582.png",
        phone: "13180273322"
        },
        {
        relationship: 0,
        userid: 7,
        stAccount: "kxr113",
        nickname: "kxr113",
        portraitUri: "http://www.sucaijishi.com/uploadfile/2016/0203/20160203022630582.png",
        phone: "15177362245"
        }
    ]
}

```
* relationship: 关系 1是好友 2不是好友
* userid: 用户ID
* stAccount: 账号
* nickname: 昵称
* portraitUri: 头像
* phone: 手机号
