# 概览

[English](overview.md) | [文档索引](README.zh-CN.md)

## 目标

可复用的 Gnalloy Pipeline 装配配方，覆盖 TCP、HTTP/1、HTTP/2、HTTP/3、WebSocket 与 MQTT。

该模块提供可复用装配配方，把 core、codec、handler 和 transport 组合成常见 Pipeline，同时保持底层模块可独立使用。

## 仓库身份

- 模块路径：`gnalloy.org/recipes`
- GitHub 仓库：`github.com/gnalloy/recipes`
- 默认分支：`dev`
- 许可证：Apache-2.0

## 包结构
- `gnalloy.org/recipes`（`recipes`）

## 直接 Gnalloy 依赖
- `gnalloy.org/gnalloy`
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`

## 当前模块规划中的直接下游
- 当前模块规划中没有其他仓库直接依赖该模块。

## 架构位置

Gnalloy 保持核心小而轻依赖。本仓库围绕单一职责形成可替换模块，通过显式 Go package 连接，而不是依靠运行时发现。

## 兼容性

公共导入路径是 `gnalloy.org/recipes`。首个稳定 tag 发布前，请按依赖策略使用 `@dev` 或明确的 pseudo-version。
