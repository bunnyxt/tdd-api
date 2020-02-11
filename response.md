# 响应格式

天钿Daily的RESTful API使用不同的[HTTP Status Code](https://www.restapitutorial.com/httpstatuscodes.html)区分不同类型的响应。

# 请求成功

若请求顺利完成，服务器将返回`200`代码，请求的资源将包含在响应体中返回。

# 请求出错

若请求出错，服务器将返回`4xx`或`5xx`代码。响应体将返回一个包含错误信息的对象。例如，访问`https://api.bunnyxt.com/tdd/v2/undefined`这样一个不存在的API地址，服务器将返回以下信息：

```JSON
{
  "code": 404,
  "message": "Not Found",
  "detail": {
    "timestamp": "2020-02-10T10:16:23.938+0000",
    "message": "No message available",
    "path": "/undefined"
  }
}
```

- code：Number，HTTP Status Code
- message：String，对错误的简要说明，或理解为对code的文字解释
- detail：Object，对错误的详细说明，是一个对象，里面可能会包含多条字段，用于详细描述错误内容

# 自定义错误代码

为了更加详细地描述错误，code字段返回的值不局限于标准HTTP Status Code。对于一些常见的错误类型，系统自定义了一些错误代码。这些错误代码为五位数，例如`40001`，前三位基于标准HTTP Status Code，表示该错误属于标准HTTP Status Code中`400`类型错误；后两位为细分类型，表示本系统中会出现的`400`错误的某一种情况，代号`01`。

## 40001 invalid request parameter

当一个请求的参数不符合规定时，服务器将返回`40001`错误。例如，访问`https://api.bunnyxt.com/tdd/v2/video?vc=2`，由于`vc`字段只能取0或1，而本次请求的vc字段的值为2，不符合API参数规定，服务器将返回以下信息。

```JSON
{
  "code": 40001,
  "message": "invalid request parameter",
  "detail": {
    "parameter": "vc",
    "value": 2,
    "prompt": "vc should be 0 or 1"
  }
}
```

# 自定义头字段

RESTful API的返回体在请求成功时只包括请求的资源，例如一个对象或对象数组，不会包含数据的元信息(meta data)，而这些信息往往又是必须的。因此，API添加了几个自定义的头字段，包含在response header中，用于返回数据元信息。

## x-total-count

`x-total-count`字段包含一个数值，表示满足该请求条件的资源的总数。由于存在单次返回对象条数限制，为了获得满足一定条件所有资源，需要搭配`pn`与`ps`字段一起使用。

例如，为获得所有VC视频，访问`https://api.bunnyxt.com/tdd/v2/video?vc=1`，只会返回前20个VC视频。查看response header中的`x-total-count`字段，为`41859`，说明总共有`41859`个VC视频，并不是只有20个VC视频，20是默认的每一页最多返回的视频个数。为了访问第21~40个VC视频，指定请求参数`pn=2`即可。注意，这里`ps`默认为20，即每一页大小为20条。若想获得第6~10个VC视频，请指定参数`ps=5&pn=2`。
