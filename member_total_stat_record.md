# member_total_stat_record - 用户视频数据总计记录

本系统收录的B站用户视频数据总计记录

字段名 | 数据类型 | 备注
:- | :- | :- 
id | Long | 主键，通用返回字段
added | Integer | 添加时间的时间戳，通用返回字段
mid | Integer | mid
video_count | Integer | 该P主参与创作的视频数量，包括自己投稿与联合投稿
view | Integer | 总播放
danmaku | Integer | 总弹幕
reply | Integer | 总评论
favorite | Integer | 总收藏
coin | Integer | 总硬币
share | Integer | 总分享
like | Integer | 总点赞

示例：[https://api.bunnyxt.com/tdd/v2/member/487708/totalstat?ps=1](https://api.bunnyxt.com/tdd/v2/member/487708/totalstat?ps=1)

```JSON
[
  {
    "id": 1,
    "added": 1573763400,
    "mid": 487708,
    "video_count": 3,
    "view": 1227623,
    "danmaku": 43656,
    "reply": 23262,
    "favorite": 54832,
    "coin": 24827,
    "share": 2839,
    "like": 8368
  }
]
```

# 根据mid查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/member/{mid}/totalstat](https://api.bunnyxt.com/tdd/v2/member/{mid}/totalstat)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
last_count | Integer | 否 | 0 | 0 <= x <= 5000 | 请求返回最后添加的x条记录，通用请求参数

> [!NOTE]
>
> 考虑到业务需求与响应性能，当且仅当设置了请求的`mid`时，`last_count`参数才有效。为了确保以上规则，`last_count`参数仅在`member/{mid}/totalstat`接口下生效，`totalstat?mid={mid}&last_count=x`是无效的。

`member/{mid}/totalstat`等价于`totalstat?mid={mid}`，除了`last_count`外，其他请求参数与响应内容等行为也完全相同，请参考[根据条件查询](#根据条件查询)。

# 根据条件查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/totalstat](https://api.bunnyxt.com/tdd/v2/totalstat)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
mid | Integer | 否 | 0 | x > 0 | UP主mid
start_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，起始，时间戳
end_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，结束，时间戳
pn | Integer | 否 | 1 | x > 0 | page num，通用请求参数
ps | Integer | 否 | 25000 | 1 < x <= 25000 | page size， 通用请求参数

> [!TIP]
> 天钿Daily所有P主会在每天北京时间凌晨4点半左右，所有视频记录爬取完之后，更新一次用户视频数据总计记录，持续时长最多半小时。如欲获得某日所有用户视频数据总计记录，设置`start_ts`为当日04:30，`end_ts`为当日05:00即可。

## 响应内容

根据请求的参数查找到的member_total_stat_record对象数组。若不存在任何满足条件的对象，则返回空数组。

响应头部包含`x-total-count`字段。

> [!WARNING]
> 若一次返回的记录条数到达page size上限25000条记录，返回体将有3.4MB左右大小，传输时间20秒左右。频繁请求过多数据将造成服务器阻塞，服务不可用。因此如有需求，需要获得大量数据，请联系站长解决。QQ群：[537793686](https://jq.qq.com/?_wv=1027&k=588s7nw)