# 发射流程内部机制

本页从调用链角度说明 SPLY 的一次发射是如何完成的。

## 1. 前端发起创建

创建页会把用户填写的项目参数与模板参数编码后发往链上入口。前端不是直接调用某个 token 合约，而是通过平台工厂体系发起创建。

## 2. TemplateFactory 接收模板级请求

`TemplateFactory` 首先判断当前模板属于哪一类：

- 平台内置模板
- 已审核通过的开发者模板
- 是否使用平台 custom core 路径
- 是否需要调用开发者自己的 core deployer

这一步的重点是把“模板选择”转化为“正确的工厂执行路径”。

## 3. LaunchFactory 创建项目主体

无论模板如何分流，最终项目主体仍由 `LaunchFactory` 组织建立。这个阶段通常会生成：

- token
- vault
- presale

如果是平台标准 token，会走标准 deployer；如果是平台 custom core，会走平台的 `CustomTokenCoreDeployer` 与 `CREATE2` 路径；如果是仍然允许的开发者自部署路径，则由模板 deployer 返回 token core。

## 4. _setup 初始化项目

`LaunchFactory` 在 `_setup()` 阶段负责把项目各部分关联起来，包括：

- 把需要的 token 数量转入 presale 路径
- 把 vault 与 presale 绑定
- 写入项目配置

这一步的关键不是简单赋值，而是把募资公式、代币数量和后续 finalize 路径对齐。

## 5. _attachTokenHooks 连接 token 与平台流程

`LaunchFactory` 还会调用 token 的平台接口，把 token 接入平台状态机，例如：

- 设置 presale
- 设置税或市场相关入口

这意味着 token core 不是独立漂浮在平台外，而是被明确接进平台流程。

## 6. 用户参与预售

用户调用 `Presale.participate()`：

- BNB 进入 `Vault`
- `Presale` 更新募集状态
- token 分配逻辑同步生效

平台当前的预售设计会把用户部分与 LP 预留部分用一致公式绑定起来，从而保证 finalize 时不需要再做一次完全不同的分配模型。

## 7. 达到条件后进入 finalize

`Presale.finalize()` 会把项目推进到公开市场状态，典型动作包括：

- 从 vault 取出可用资金
- 处理平台费
- 用预留 token 和 paired asset 建立 LP
- 获取 pair 地址
- 把 pair 写入 token market config
- 销毁 LP
- 开启交易
- 锁定关键参数
- 放弃临时权限
- 清空 presale 地址

这一步是 SPLY 最关键的系统价值所在。平台把“开盘后应该自动进入的状态”写成了协议路径。

## 8. 后端监听 finalized 项目

项目 finalize 后，后端 watcher 会扫描最新 finalized 项目，并把 token 推入自动验证队列。

## 9. 前台与外部平台消费公开状态

前台项目页与代币页，后端 API，以及外部扫描平台，最终看到的是 finalize 后的公开状态组合。平台的职责不是控制第三方展示结果，而是尽量提供统一、清晰、可验证的链上输入。

## 为什么这条调用链重要

如果没有这套内部组织，平台看起来只是“页面 + 合约”，但实际上会退化成：

- 模板自己部署
- 模板自己募资
- 模板自己处理 LP
- 平台只负责做 UI

SPLY 当前的设计重点就是避免这种退化。
