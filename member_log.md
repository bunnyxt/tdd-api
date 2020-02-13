# member_log - 用户信息更新日志

本系统收录的用户的信息更新日志

字段名 | 数据类型 | 备注
:- | :- | :- 
id | Long | 主键，通用返回字段
added | Integer | 添加时间的时间戳，通用返回字段
mid | Integer | 用户mid
attr | String | 发生变动的字段
oldval | String | 字段变更前的值
newval | String | 字段变更后的值

示例：[https://api.bunnyxt.com/tdd/v2/member/log?mid=12661425](https://api.bunnyxt.com/tdd/v2/member/log?mid=12661425)

```JSON
[
  {
    "id": 10675,
    "added": 1581610695,
    "mid": 12661425,
    "attr": "face",
    "oldval": "http://i1.hdslb.com/bfs/face/316fc1378d5fbdaf7bc4878e35a282b7dcd2f50b.jpg",
    "newval": "http://i2.hdslb.com/bfs/face/316fc1378d5fbdaf7bc4878e35a282b7dcd2f50b.jpg"
  },
  {
    "id": 10676,
    "added": 1581610695,
    "mid": 12661425,
    "attr": "sign",
    "oldval": "微博@齐亦橙-与天依心跳同步的时光，继续努力吧，未来一定会比梦想更加灿烂！！！",
    "newval": "微博@齐亦橙，继续努力吧，未来一定会比梦想更加灿烂！！！"
  }
]
```

# 根据条件查询

## URL

GET：[https://api.bunnyxt.com/tdd/v2/member/log](https://api.bunnyxt.com/tdd/v2/member/log)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
mid | Integer | 否 | 0 | x > 0 | 用户mid
start_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，起始，时间戳
end_ts | Integer | 否 | 无 | x > 0 | 记录添加时间，结束，时间戳
attr | String | 否 | 无 | / | 发生变动的字段
oldval | String | 否 | 无 | / | 字段变更前的值（包含该部分）
newval | String | 否 | 无 | / | 字段变更后的值（包含该部分）
pn | Integer | 否 | 1 | x > 0 | page num，通用请求参数
ps | Integer | 否 | 20 | 1 < x <= 20 | page size， 通用请求参数

其中`attr`参数应为`member`对象的某一属性，详情请参考[member - 用户](member.md)。

## 响应内容

根据请求的参数查找到的member_log对象数组。若不存在任何满足条件的对象，则返回空数组。

响应头部包含`x-total-count`字段。

> [!NOTE]
> `face`属性发生更改，并不意味着该用户更换了头像。例如上面示例中：
> 
> > "oldval": "http://i1.hdslb.com/bfs/face/316fc1378d5fbdaf7bc4878e35a282b7dcd2f50b.jpg"
> > 
> >"newval": "http://i2.hdslb.com/bfs/face/316fc1378d5fbdaf7bc4878e35a282b7dcd2f50b.jpg"
> 
> 可以看到，新旧URL只有子域名不同（`i1` -> `i2`），定位到的图片名（`316fc1378d5fbdaf7bc4878e35a282b7dcd2f50b.jpg`）完全相同，打开后图片也是同一张，推测可能是资源服务器的调整等因素。只有定位到的图片名不同时，才说明该用户更换了头像。