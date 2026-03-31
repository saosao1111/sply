# API 参考

本页列出平台当前主要公开接口与管理接口，重点说明用途与输入输出方向，而不是逐字段列出全部内部实现。

## Public APIs

## `GET /api/projects`

用途：

- 获取公开项目列表
- 首页、项目列表页主要使用该接口

典型返回内容：

- 项目基础信息
- 募资进度
- 项目状态
- 模板与代币映射信息

## `GET /api/project/:id`

用途：

- 获取单项目详情
- 项目页主要使用该接口

典型返回内容：

- 项目配置
- 募资数据
- token / presale / pair 关联信息
- 页面展示所需资料

## `GET /api/token/:addr`

用途：

- 获取单 token 元数据

典型返回内容：

- token 对应项目信息
- token 公开元数据

## `GET /api/token-market/:address`

用途：

- 获取 token 市场快照

典型返回内容：

- 价格
- 市值估算
- pair 信息
- market phase 相关数据

## `GET /api/token-liquidity/:address`

用途：

- 获取流动性相关数据

典型返回内容：

- LP 储备
- 锁定状态相关信息
- 流动性估算

## `GET /api/token-trades/:address`

用途：

- 获取最近交易列表

典型返回内容：

- 买卖记录
- 时间戳
- 交易方向
- 成交数量

## Content APIs

## `POST /api/upload`

用途：

- 上传项目 logo 等素材

## `POST /api/save-metadata`

用途：

- 保存项目的对外展示元数据

## Developer Submission APIs

## `POST /api/dev-submit`

用途：

- 提交开发者模板审核

## `GET /api/dev-submissions`

用途：

- 获取模板提交记录

## Admin APIs

## `GET /api/admin/nonce`

用途：

- 获取管理员登录 nonce

## `POST /api/admin/login`

用途：

- 管理员登录

## `POST /api/admin/logout`

用途：

- 管理员退出

## `GET /api/admin/stats`

用途：

- 获取后台统计信息

## `POST /api/admin/dev-review`

用途：

- 审核并注册开发者模板

## `POST /api/admin/verify-token`

用途：

- 手动触发源码验证

## `POST /api/admin/project/hide`

用途：

- 隐藏项目，不在前台公开展示

## 接口使用建议

- 面向前台页面开发时，优先使用平台 API，而不是自己从链上重建所有视图
- 面向更底层监控或索引时，可以把 API 作为辅助层，链上读取作为最终校验
