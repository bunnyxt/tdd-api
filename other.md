# other - 其他

其他杂项API。这里的API参数与格式相对比较随意，可能与其他API不同，请认真阅读。

> 已下线：`statdaily - 每日记录`（`GET /tdd/v2/statdaily`）接口已移除。其数据来源（每日全站计数任务）已停止，该接口不再提供服务，依赖它的首页统计展示也已下线。

# updatelog - 更新日志

## URL

GET：[https://api.bunnyxt.com/tdd/v2/updatelog](https://api.bunnyxt.com/tdd/v2/updatelog)

## 请求参数

参数名 | 数据类型 | 是否必须 | 默认值 | 取值范围 | 备注
:- | :- | :- | :- | :- | :-
last_count | Integer | 否 | 5 | x >= 0 | 最近的日志的条数，**0表示获取所有日志**

## 响应内容

updatelog为系统更新日志记录，由站长手动维护，只记录较大更新事件。

updatelog对象结构如下：

字段名 | 数据类型 | 备注
:- | :- | :- 
added | Integer | 添加时间的时间戳，通用返回字段
type | Integer | 更新类型，1：添加；2：删除；3：修改
content | String | 日志内容

根据请求的参数查找到的updatelog对象数组。若不存在任何满足条件的对象，则返回空数组。

示例：[https://api.bunnyxt.com/tdd/v2/updatelog?last_count=2](https://api.bunnyxt.com/tdd/v2/updatelog?last_count=2)

```JSON
[
  {
    "added": 1581238268,
    "type": 1,
    "content": "添加视频封面上的视频tag显示。"
  },
  {
    "added": 1581083526,
    "type": 1,
    "content": "添加周刊自动算分功能，整合到视频详情页面。"
  }
]
```