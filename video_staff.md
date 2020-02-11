# video_staff - 视频staff

本系统收录的视频staff

字段名 | 数据类型 | 备注
- | - | - 
mid | Integer | mid
name | String | 昵称
face | String | 头像url
title | String | 分工

示例：[https://api.bunnyxt.com/tdd/v2/video/78977256/staff](https://api.bunnyxt.com/tdd/v2/video/78977256/staff)

```JSON
[
  {
    "mid": 43855,
    "name": "litterzy",
    "face": "http://i1.hdslb.com/bfs/face/e026493863004b4ad37f9585be61c71e24e1dc71.jpg",
    "title": "UP主"
  },
  {
    "mid": 541480,
    "name": "填词的那个Vagary",
    "face": "http://i1.hdslb.com/bfs/face/1041b8f5c654d3fa91a9b8f4e24cb0356eb07f78.jpg",
    "title": "作词"
  },
  {
    "mid": 3241451,
    "name": "Creuzer",
    "face": "http://i2.hdslb.com/bfs/face/79079ff6377871eb7d01d64b2f6d08a2fc448d5e.jpg",
    "title": "调校"
  }
]
```

# 根据aid获取

## URL

GET：[https://api.bunnyxt.com/tdd/v2/video/78977256/staff](https://api.bunnyxt.com/tdd/v2/video/78977256/staff)

## 请求参数

URL参数 | 数据类型 | 取值范围 | 备注
- | - | - | -
aid | Integer | x > 0 | 视频aid

## 响应内容

根据给定的aid查找到的该视频的staff组成的video_staff对象数组。若该aid不存在staff，则返回空数组。