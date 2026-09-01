# recipes

[English](README.md) | [文档](docs/README.zh-CN.md)

可复用的 Gnalloy Pipeline 装配配方，覆盖 TCP、HTTP/1、HTTP/2、HTTP/3、WebSocket 与 MQTT。

该模块提供可复用装配配方，把 core、codec、handler 和 transport 组合成常见 Pipeline，同时保持底层模块可独立使用。

## 状态

- 导入路径：`gnalloy.org/recipes`
- 仓库：`github.com/gnalloy/recipes`
- 默认分支：`dev`
- 预览安装：`go get gnalloy.org/recipes@dev`
- 许可证：Apache-2.0

## 安装
```bash
go get gnalloy.org/recipes@dev
go doc gnalloy.org/recipes
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
```

## 文档
- [概览](docs/overview.zh-CN.md) ([English](docs/overview.md))
- [用法](docs/usage.zh-CN.md) ([English](docs/usage.md))
- [案例](docs/examples.zh-CN.md) ([English](docs/examples.md))
- [配置说明](docs/configuration.zh-CN.md) ([English](docs/configuration.md))
- [测试与性能](docs/testing.zh-CN.md) ([English](docs/testing.md))
- [API 参考](docs/api.zh-CN.md) ([English](docs/api.md))
- [注意事项与备注](docs/notes.zh-CN.md) ([English](docs/notes.md))
- [ADR-001 模块边界](docs/decisions/0001-module-boundary.zh-CN.md) ([English](docs/decisions/0001-module-boundary.md))

## 模块边界

本仓库负责：可复用的 Gnalloy Pipeline 装配配方，覆盖 TCP、HTTP/1、HTTP/2、HTTP/3、WebSocket 与 MQTT。

它不吸收相邻模块职责。核心基础能力保留在 `gnalloy.org/gnalloy`；协议 codec、transport、handler、resolver、examples 与 benchmarks 分别由独立仓库负责。

## 包结构
- `gnalloy.org/recipes`（`recipes`）

## Gnalloy 依赖

- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`
- `gnalloy.org/gnalloy`

## 常见集成方式
- 配置通过显式构造函数和 option struct 传入，不使用包级可变状态。
- 热路径默认值必须保守、有界，并注意分配成本。
- Raw IP 路径通常需要管理员权限，或在支持 raw socket 的系统上授予 `CAP_NET_RAW`。

## 当前公共入口

生成的 API 参考列出了完整公共面。当前常用构造函数或 option 类型包括：
- `const HandlerNameHTTP1RequestDecoder = "http1-request-decoder" ...`
- `const HandlerNameMQTTFrameDecoder = "mqtt-frame-decoder" ...`
- `const HandlerNameByteBufEcho = "bytebuf-echo" ...`
- `const HandlerNameWebSocketHandshake = "websocket-handshake" ...`
- `var ErrInvalidRecipe = errors.New("gnalloy/recipes: invalid recipe")`
- `type HTTP1Config struct{ ... }`
- `type HTTP2Config struct{ ... }`
- `type LengthFieldConfig struct{ ... }`
- `type LineConfig struct{ ... }`
- `type MQTTConfig struct{ ... }`
- `type WebSocketServerConfig struct{ ... }`

## 验证

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
GOWORK=off GOTOOLCHAIN=local go vet ./...
GOWORK=off GOTOOLCHAIN=local go test ./... -run '^$' -bench . -benchmem -count=1
```

压测时，将该模块和相应 transport、codec、handler 栈装配后，使用 `gnalloy.org/benchmarks` 或 `gnalloy.org/examples` 中的场景运行。报告必须保留主机、操作系统、payload、并发度、warmup 和 repetition。

## 注意事项
- 本仓库保持窄边界。跨模块行为应在应用、recipes、examples 或 benchmark harness 中装配。
- 公共 API 必须保持 Go 原生和显式；热路径避免运行时扫描、隐藏全局注册表和重反射。
- 网络输入一律视为不可信。配置解析上限，返回类型化错误，不使用 panic 处理输入错误。
- 性能结论必须绑定具体主机、操作系统、协议、payload、并发度、warmup 和 repetition。
