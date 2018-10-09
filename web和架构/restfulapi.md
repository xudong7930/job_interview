Reustful api
===========


#返回结果的结构
```json
{
    data : { // 请求数据，对象或数组均可
        user_id: 123,
        user_name: "tutuge",
        user_age: 23,
        user_avatar_url: "http://tutuge.me/avatar.jpg"
    },
    msg : "done", // 请求状态描述，调试用: done|error
    code: 1001, // 业务自定义状态码
    extra : { // 全局附加数据，字段、内容不定
        type: 1,
        desc: "签到成功！"
    }
}

```

#返回状态码:
```
// Code 业务自定义状态码定义示例
 
// 授权相关
1001: 无权限访问
1002: access_token过期
1003: unique_token无效

// 用户相关
2001: 未登录
2002: 用户信息错误
2003: 用户不存在
 
// 业务1
3001: 业务1XXX
3002: 业务1XXX

```


#字段统一:
```
// 字符串
user_name, task_desc, date_str, article_title, feed_content 等
 
// 数字
user_id, users_count, task_num, xxx_offset 等
 
// 日期
login_at, create_date, logout_time 等
 
// 布尔
is_done, is_vip, protected, can_read 等
 
// URL
user_avatar_url, thumb_url 等
 
// 数组
users, profiles, thumb_imgs 等
```


#空值、空字段的处理
```
数字: 0
字符串: ""
数组: [],
对象: {}
布尔值: 0,1
时间日期: 1462068610
```

# restful安全
```
#方式1
1.获取排序后的参数: sorted_params
2.对排序后的参数签名: hmac_sha1(sorted_params + oauth_secret)

#方式2
https+header中加令牌

#方式3:
oauth授权
```

