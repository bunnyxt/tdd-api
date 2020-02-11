# 项目介绍

[天钿Daily](https://tdd.bunnyxt.com)（TianDian Daily）是一个VC相关数据交流与分享的网站。天钿Daily致力于VC相关数据交流，基于B站API以及简单的网络爬虫，定期抓取VC相关数据，选取有意义的纬度展示。

# 技术架构

天钿Daily使用前后端分离技术，初版后端（v1）使用PHP编写。考虑到业务扩展需要，新版后端（v2）使用Spring Boot构建RESTful API，并且将逐步替代初版后端。因此，本文档只介绍v2版本后端接口。

后端采用RESTful API架构，但由于作者能力有限，存在部分不严格遵循规范之处，还请谅解。

该文档使用GitBook编写，部署在[https://api.bunnyxt.com/tdd/doc/](https://api.bunnyxt.com/tdd/doc/)此处。请访问以上URL以获得最佳阅读体验。

# 使用须知

使用本站API、数据，意味着您知晓并同意以下内容：

- 天钿Daily的数据抓取自B站公开API，不会收集任何敏感信息。本着数据交流与分享的目的，这些数据将会在最大的程度上开放。
- 任何人都可以使用API获取数据。绝大多数数据相关API不需要身份认证即可访问，部分本站私有用户数据除外。
- API没有做访问速率限制，**禁止爆破、请勿滥用**。
- 所有使用到本站数据的作品，包括但不限于程序、应用、文章、视频等，必须注明数据来源为天钿Daily。
- 由于存在不可避免的网络问题或程序问题，本站无法保证所有数据的绝对可靠。若您因为本站的信息直接或间接蒙受任何损失，本站将不负任何责任。
- 本站对所有数据持中立态度，不发表也不鼓励基于数据的，对任何实体，包括作品、P主、社团、歌姬等的任何片面评价。数据受到多方面因素的影响，实体的评价也应该综合全面。

# 联系我们

- QQ群：[537793686](https://jq.qq.com/?_wv=1027&k=588s7nw)
- 个人邮箱：[bunnyxt@outlook.com](bunnyxt@outlook.com)

# 链接

- GitHub Project：[TianDian Daily](https://github.com/users/bunnyxt/projects/1)
- 前端：[tdd-frontend](https://github.com/bunnyxt/tdd-frontend)
- 后端：[tdd-backend](https://github.com/bunnyxt/tdd-backend)
- 爬虫：[tdd-spider](https://github.com/bunnyxt/tdd-spider)