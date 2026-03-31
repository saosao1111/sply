# 架构与组件

## 总体结构

SPLY 当前可以理解成三层系统：

## 1. 链上协议层

链上协议层负责项目创建、资金托管、预售状态、模板路由、市场进入和权限收口。核心组件包括：

- `LaunchFactory`
- `TemplateFactory`
- `FactoryAdmin`
- `Presale`
- `Vault`
- token core
- 各类 deployer

## 2. 后端服务层

后端负责聚合项目数据、提供 API、执行自动验证、管理后台认证与审核数据，并把链上状态整理成前台可消费的接口。

## 3. 前端产品层

前端负责展示首页、创建页、模板页、项目页、代币页和后台审核页。它不是链上协议的简单壳，而是用户与项目状态的主要交互层。

## 核心合约角色

## LaunchFactory

`LaunchFactory` 是项目主体工厂。它负责：

- 创建 token、vault、presale
- 调用 `_setup()` 进行项目初始化
- 调用 `_attachTokenHooks()` 把 token 与 presale/strategy 关联起来
- 维护标准 token 和自定义 token core 的部署路径
- 管理内置 token 盐池与 custom core 盐池

它是“项目生成器”，不是模板审核器。

## TemplateFactory

`TemplateFactory` 负责模板分流与模板入口。它判断当前模板属于哪一类：

- 平台内置模板
- 已审核通过的开发者模板
- 使用平台 custom core 路径的模板
- 使用开发者自部署 core 路径的模板

它是“模板路由器”，不是资金托管合约。

## FactoryAdmin

`FactoryAdmin` 负责开发者模板治理：

- 注册模板
- 开关模板
- 记录 capability flags 与 schema 约束
- 紧急关闭仍处于募资状态的项目

它是“模板管理器”，不是项目创建器。

## Presale

`Presale` 负责募资状态机：

- 接收参与
- 记录募集进度
- 在满足条件时触发 finalize
- 与 Vault 和 token 协同完成项目收口

它是“项目生命周期控制器”，不是钱包。

## Vault

`Vault` 负责预售资金托管。其设计重点是：

- 平台模板无法直接绕开 Vault 取走募集资金
- 资金释放必须服从 Presale 状态
- 可退款与可 finalize 的路径是明确分开的

它是“资金边界”，不是代币逻辑扩展点。

## token core

token core 是代币行为所在的位置。它决定：

- 代币状态变量
- 转账逻辑
- 税逻辑
- 权限控制
- 与 market config 相关的行为

在内置模板里，token core 由平台控制；在开发者模板里，token core 可以扩展，但必须满足平台接口规范。

## deployer

deployer 是模板部署入口。对于开发者模板，平台关心的不只是“部署一个合约”，而是 deployer 是否：

- 按平台接口解码参数
- 能返回可验证的 token core
- 能被平台审核和注册

## 权限拆分

当前正式架构里，平台采用了分层 ownership：

- `Factory` 与 `TemplateFactory` 归多签控制
- `FactoryAdmin` 可以交给更灵活的运营钱包

这种拆分的意义是：

- 核心发射路径仍由更高安全级别控制
- 模板审核与模板上架可以更灵活
- 不需要把所有链上管理动作都绑在同一个 owner 上

## 平台为什么要这样拆

如果没有这层拆分，平台很容易出现两种坏结果：

- 所有模板能力都被锁死，扩展太慢
- 或者模板权限太高，平台边界失控

SPLY 当前架构是在“开放模板能力”和“保持平台标准”之间取一个平衡。
