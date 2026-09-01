# 案例

[English](examples.md) | [文档索引](README.zh-CN.md)

## 案例 1：将模块加入应用

```bash
mkdir gnalloy-app && cd gnalloy-app
go mod init example.com/gnalloy-app
go get gnalloy.org/recipes@dev
go doc gnalloy.org/recipes
```

## 案例 2：查看当前包

当前源码树暴露这些 package 导入路径：
- `gnalloy.org/recipes`

按需要的行为对对应 package 执行 `go doc`：

```bash
go doc gnalloy.org/recipes
```

精选当前导出入口：
- `const HandlerNameHTTP1RequestDecoder = "http1-request-decoder" ...`
- `const HandlerNameMQTTFrameDecoder = "mqtt-frame-decoder" ...`
- `const HandlerNameByteBufEcho = "bytebuf-echo" ...`
- `const HandlerNameWebSocketHandshake = "websocket-handshake" ...`
- `var ErrInvalidRecipe = errors.New("gnalloy/recipes: invalid recipe")`
- `func Apply(ch channel.Channel, specs ...HandlerSpec) error`

## 案例 3：将可执行测试作为行为示例

仓库测试是受支持行为的可执行示例。先从下面的精选名称开始，再阅读对应 `_test.go` 文件中的完整 setup 和断言。完整发现列表见 [测试与性能](testing.zh-CN.md)。

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -run Test -count=1
```

精选当前 test、benchmark、fuzz 与 example 入口：
- `TestHTTP1ServerRecipe`
- `TestHTTP2ConnectionRecipeInstallsPipeline`
- `TestInitializerRollsBackOnFactoryError`
- `TestLengthFieldFramesRoundTrip`
- `TestMQTTFramesRecipe`
- `TestWebSocketServerRecipeUpgrade`

## 案例 4：跨模块装配

本模块的直接 Gnalloy 依赖：
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`
- `gnalloy.org/gnalloy`

装配说明：
- recipes 作为常见 Gnalloy 栈的可复用装配指导。
- recipe 应依赖公开模块契约，不应隐藏生产策略。
- 复制到服务前，需要为每个 recipe 跑集成场景和压测场景。

## 案例 5：压测 Harness

持续负载测试时，如果该模块参与网络流量路径，将它接入 `gnalloy.org/benchmarks` 的场景，或接入 `gnalloy.org/examples` 的可运行客户端。报告中记录 host、OS、CPU、Go version、protocol、payload、concurrency、warmup、repetitions、throughput 和 p99 latency。
