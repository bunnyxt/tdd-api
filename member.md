# member - 用户

本系统收录的用户

字段名 | 数据类型 | 备注
:- | :- | :- 
id | Long | 主键，通用返回字段
added | Integer | 添加时间的时间戳，通用返回字段
mid | Integer | mid
sex | String | 性别
name | String | 昵称
face | String | 头像url
sign | String | 个性签名

示例：[https://api.bunnyxt.com/tdd/v2/member/487708](https://api.bunnyxt.com/tdd/v2/member/487708)

```JSON
{
  "id": 1,
  "added": 1554020874,
  "mid": 487708,
  "sex": "男",
  "name": "唐乐林",
  "face": "http://i0.hdslb.com/bfs/face/58e830e42273f16ee4133318c43acad106d76914.jpg",
  "sign": "默默守望，希望天依越来越好~"
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
pn | Integer | 否 | 1 | x > 0 | page num，通用请求参数
ps | Integer | 否 | 20 | 1 < x <= 20 | page size， 通用请求参数

## 响应内容

根据请求的参数查找到的member对象数组。若不存在任何满足条件的对象，则返回空数组。

响应头部包含`x-total-count`字段。
