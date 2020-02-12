# video_record - 视频记录

本系统爬取的视频记录

字段名 | 数据类型 | 备注
:- | :- | :- 
id | Long | 主键，通用返回字段
added | Integer | 添加时间的时间戳，通用返回字段
aid | Integer | aid
view | Integer | 播放
danmaku | Integer | 弹幕
reply | Integer | 评论
favorite | Integer | 收藏
coin | Integer | 硬币
share | Integer | 分享
like | Integer | 点赞

示例：[https://api.bunnyxt.com/tdd/v2/video/456930/record?ps=1](https://api.bunnyxt.com/tdd/v2/video/456930/record?ps=1)

```JSON
[
  {
    "id": 189462,
    "added": 1572620367,
    "aid": 456930,
    "view": 1018605,
    "danmaku": 37440,
    "reply": 22275,
    "favorite": 48314,
    "coin": 22626,
    "share": 2629,
    "like": 7498
  }
]
```

# 根据aid查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/video/{aid}/record](https://api.bunnyxt.com/tdd/v2/video/{aid}/record)

`video/{aid}/record`等价于`record?aid={aid}`，其他请求参数与响应内容等行为也完全相同，请参考[根据条件查询](#根据条件查询)。

# 根据条件查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/record](https://api.bunnyxt.com/tdd/v2/record)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
aid | Integer | 否 | 0 | x > 0 | 视频aid
start_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，起始，时间戳
end_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，结束，时间戳
pn | Integer | 否 | 1 | x > 0 | page num，通用请求参数
ps | Integer | 否 | 25000 | 1 < x <= 25000 | page size， 通用请求参数

> [!TIP]
> 天钿Daily所有视频会在每天北京时间凌晨4点更新一次所有视频的记录，持续时长半小时左右。如欲获得某日所有视频的记录，设置`start_ts`为当日04:00，`end_ts`为当日04:30即可。

## 响应内容

根据请求的参数查找到的video_record对象数组。若不存在任何满足条件的对象，则返回空数组。

响应头部包含`x-total-count`字段。

> [!WARNING]
> 若一次返回的记录条数到达page size上限25000条记录，返回体将有3MB左右大小，传输时间20秒左右。频繁请求过多数据将造成服务器阻塞，服务不可用。因此如有需求，需要获得大量数据，请联系站长解决。QQ群：[537793686](https://jq.qq.com/?_wv=1027&k=588s7nw)