# recipes

可复用的 Gnalloy Pipeline 装配配方，覆盖 TCP、HTTP/1、HTTP/2、HTTP/3、WebSocket 与 MQTT。

本仓库属于 Gnalloy 模块化网络栈。默认分支是 `dev`；本次初始化不创建 release，不打 tag。

## 安装

```bash
go get gnalloy.org/recipes@dev
```

## 模块边界

- 模块路径：`gnalloy.org/recipes`
- 职责：可复用的 Gnalloy Pipeline 装配配方，覆盖 TCP、HTTP/1、HTTP/2、HTTP/3、WebSocket 与 MQTT
- 核心依赖：需要 Gnalloy ByteBuf、Channel、EventLoop 或 Bootstrap 契约时依赖 `gnalloy.org/gnalloy`。

## Gnalloy 依赖

- `gnalloy.org/gnalloy`
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`

## 开发验证

```bash
go test ./... -count=1
go vet ./...
go test ./... -run '^$' -bench . -benchmem -benchtime=100ms -count=1
```

跨仓库开发使用 `G:\opensource\gnalloy\go.work`。独立模块复验时设置 `GOWORK=off`。

## 许可证

Apache-2.0。
