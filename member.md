# member - 用户

本系统收录的B站用户

字段名 | 数据类型 | 备注
:- | :- | :- 
id | Long | 主键，通用返回字段
added | Integer | 添加时间的时间戳，通用返回字段
mid | Integer | mid
sex | String | 性别
name | String | 昵称
face | String | 头像url
sign | String | 个性签名
video_count | Integer | 该P主参与创作的视频数量，包括自己投稿与联合投稿
last_video | Object | 最新投稿视频信息
last_total_stat | Object | 最新P主视频数据总计信息
last_follower | Object | 最新P主粉丝数信息

其中：

`last_video`对象，即[video](video.md)对象的一部分

字段名 | 数据类型 | 备注
:- | :- | :- 
aid | Integer | aid
pic | String | 封面图片url
title | String | 标题
pubdate | Integer | 发布时间的时间戳
mid | Integer | UP主mid
laststat | Object | 最近一次更新的数据，若无则为null

`last_total_stat`对象，即[member_last_total_stat_record](member_last_total_stat_record.md)对象的一部分

字段名 | 数据类型 | 备注
:- | :- | :- 
added | Integer | 添加时间的时间戳，通用返回字段
video_count | Integer | 该P主参与创作的视频数量，包括自己投稿与联合投稿
view | Integer | 总播放
danmaku | Integer | 总弹幕
reply | Integer | 总评论
favorite | Integer | 总收藏
coin | Integer | 总硬币
share | Integer | 总分享
like | Integer | 总点赞

`last_follower`对象，即[member_last_follower_record](member_last_follower_record.md)对象的一部分

字段名 | 数据类型 | 备注
:- | :- | :- 
added | Integer | 添加时间的时间戳，通用返回字段
follower | Integer | 粉丝数

示例：[https://api.bunnyxt.com/tdd/v2/member/487708](https://api.bunnyxt.com/tdd/v2/member/487708)

```JSON
{
  "id": 1,
  "added": 1554020874,
  "mid": 487708,
  "sex": "男",
  "name": "唐乐林",
  "face": "http://i0.hdslb.com/bfs/face/58e830e42273f16ee4133318c43acad106d76914.jpg",
  "sign": "默默守望，希望天依越来越好~",
  "video_count": 3,
  "last_video": {
    "aid": 456930,
    "pic": "http://i1.hdslb.com/bfs/archive/4d77551f38628061bd872b3eeffbfab6e1cbe55e.jpg",
    "title": "【洛天依】前尘如梦「新年重制版」（By桜色妖精）",
    "pubdate": 1359631780,
    "mid": 487708,
    "laststat": {
      "added": 1582230191,
      "view": 1032603,
      "danmaku": 37526,
      "reply": 23200,
      "favorite": 48738,
      "coin": 23326,
      "share": 2718,
      "like": 8410
    }
  },
  "last_total_stat": {
    "added": 1582231501,
    "video_count": 3,
    "view": 1242514,
    "danmaku": 43738,
    "reply": 24076,
    "favorite": 55299,
    "coin": 25565,
    "share": 2925,
    "like": 9349
  },
  "last_follower": {
    "added": 1582229450,
    "follower": 4224
  }
}
```

# 根据mid获取

## URL

GET：[https://api.bunnyxt.com/tdd/v2/member/{mid}](https://api.bunnyxt.com/tdd/v2/member/{mid})

## 请求参数

URL参数 | 数据类型 | 取值范围 | 备注
:- | :- | :- | :-
mid | Integer | x > 0 | 用户mid

## 响应内容

根据给定的mid查找到的一个member对象。若不存在该mid的对象，则返回空。

# 根据条件查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/member](https://api.bunnyxt.com/tdd/v2/member)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
sex | String | 否 | 无 | [男, 女, 保密] | 用户性别
name | String | 否 | 无 | / | 用户昵称（包含该部分）
order_by | String | 否 | pubdate | [mid, video_count, v_pubdate, sr_view, sr_danmaku, sr_reply, sr_favorite, sr_coin, sr_share, sr_like, fr_follower] | 排序依据
desc | Integer | 否 | 1 | 0, 1 | 排序，0：从小到大；1：从大到小
pn | Integer | 否 | 1 | x > 0 | page num，通用请求参数
ps | Integer | 否 | 20 | 1 < x <= 20 | page size， 通用请求参数

## 响应内容

根据请求的参数查找到的member对象数组。若不存在任何满足条件的对象，则返回空数组。

响应头部包含`x-total-count`字段。

# 随机用户

## URL

GET：[https://api.bunnyxt.com/tdd/v2/member/random](https://api.bunnyxt.com/tdd/v2/member/random)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
count | Integer | 否 | 1 | 1 <= x <= 20 | 获取用户个数

## 响应内容

随机`count`个用户构成的member对象数组。

> [!NOTE]
> 并非在所有收录的UP主中随机，是在一个单独的经过筛选的所有UP主的一个子集中随机抽取。该子集收录标准为：参与创作的视频数>=3，总播放量>=30000。