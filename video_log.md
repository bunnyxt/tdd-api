# video_log - 视频信息更新日志

本系统收录的视频的信息更新日志

字段名 | 数据类型 | 备注
:- | :- | :- 
id | Long | 主键，通用返回字段
added | Integer | 添加时间的时间戳，通用返回字段
aid | Integer | 视频aid
attr | String | 发生变动的字段
oldval | String | 字段变更前的值
newval | String | 字段变更后的值

示例：[https://api.bunnyxt.com/tdd/v2/video/log?aid=34644911](https://api.bunnyxt.com/tdd/v2/video/log?aid=34644911)

```JSON
[
  {
    "id": 1662,
    "added": 1581523276,
    "aid": 34644911,
    "attr": "pic",
    "oldval": "http://i0.hdslb.com/bfs/archive/e26eca8b674dfc79fb173f0aa760730c82e88900.jpg",
    "newval": "http://i1.hdslb.com/bfs/archive/4e80dfc49055c1adb7dc1e191f5fec614ef99583.jpg"
  },
  {
    "id": 1663,
    "added": 1581523276,
    "aid": 34644911,
    "attr": "title",
    "oldval": "我不想打工",
    "newval": "打        工       奇      才"
  },
  {
    "id": 1664,
    "added": 1581523276,
    "aid": 34644911,
    "attr": "hasstaff",
    "oldval": "-1",
    "newval": "0"
  }
]
```

# 根据条件查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/video/log](https://api.bunnyxt.com/tdd/v2/video/log)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
aid | Integer | 否 | 0 | x > 0 | 视频aid
start_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，起始，时间戳
end_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，结束，时间戳
attr | String | 否 | 无 | / | 发生变动的字段
oldval | String | 否 | 无 | / | 字段变更前的值（包含该部分）
newval | String | 否 | 无 | / | 字段变更后的值（包含该部分）
pn | Integer | 否 | 1 | x > 0 | page num，通用请求参数
ps | Integer | 否 | 20 | 1 < x <= 20 | page size， 通用请求参数

其中`attr`参数应为`video`对象的某一属性，详情请参考[video - 视频](video.md)。

## 响应内容

根据请求的参数查找到的video_log对象数组。若不存在任何满足条件的对象，则返回空数组。

响应头部包含`x-total-count`字段。
