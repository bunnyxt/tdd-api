# member_follower_record - 用户粉丝记录

本系统爬取的本系统收录的B站用户的粉丝数记录

字段名 | 数据类型 | 备注
:- | :- | :- 
id | Long | 主键，通用返回字段
added | Integer | 添加时间的时间戳，通用返回字段
mid | Integer | mid
follower | Integer | 粉丝数

示例：[https://api.bunnyxt.com/tdd/v2/member/487708/follower?ps=1](https://api.bunnyxt.com/tdd/v2/member/487708/follower?ps=1)

```JSON
[
  {
    "id": 2886,
    "added": 1581851996,
    "mid": 487708,
    "follower": 4223
  }
]
```

# 根据mid查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/member/{mid}/follower](https://api.bunnyxt.com/tdd/v2/member/{mid}/follower)

`member/{mid}/record`等价于`follower?mid={mid}`，其他请求参数与响应内容等行为也完全相同，请参考[根据条件查询](#根据条件查询)。

# 根据条件查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/follower](https://api.bunnyxt.com/tdd/v2/follower)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
mid | Integer | 否 | 0 | x > 0 | UP主mid
start_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，起始，时间戳
end_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，结束，时间戳
pn | Integer | 否 | 1 | x > 0 | page num，通用请求参数
ps | Integer | 否 | 25000 | 1 < x <= 25000 | page size， 通用请求参数

> [!TIP]
> 天钿Daily所有P主会在每天北京时间凌晨4点更新一次粉丝数记录，持续时长两小时多一点。如欲获得某日所有P主的粉丝数记录，设置`start_ts`为当日04:00，`end_ts`为当日06:15即可。

## 响应内容

根据请求的参数查找到的member_follower_record对象数组。若不存在任何满足条件的对象，则返回空数组。

响应头部包含`x-total-count`字段。

> [!WARNING]
> 若一次返回的记录条数到达page size上限25000条记录，返回体将有1.4MB左右大小，传输时间10秒左右。频繁请求过多数据将造成服务器阻塞，服务不可用。因此如有需求，需要获得大量数据，请联系站长解决。QQ群：[537793686](https://jq.qq.com/?_wv=1027&k=588s7nw)