# API 参考

[English](api.md) | [文档索引](README.zh-CN.md)

本清单由本仓库 package 的 `go doc -short` 生成，用于快速查看公共面。精确语义以源码和测试为准。

## 包

### `gnalloy.org/recipes`

包名：`recipes`

```text
const HandlerNameHTTP1RequestDecoder = "http1-request-decoder" ...
const HandlerNameMQTTFrameDecoder = "mqtt-frame-decoder" ...
const HandlerNameByteBufEcho = "bytebuf-echo" ...
const HandlerNameWebSocketHandshake = "websocket-handshake" ...
var ErrInvalidRecipe = errors.New("gnalloy/recipes: invalid recipe")
func Apply(ch channel.Channel, specs ...HandlerSpec) error
func ByteBufEcho() bootstrap.ChildInitializer
func HTTP1Client(cfg HTTP1Config, app ...HandlerSpec) bootstrap.ChildInitializer
func HTTP1Server(cfg HTTP1Config, app ...HandlerSpec) bootstrap.ChildInitializer
func HTTP2Connection(cfg HTTP2Config, app ...HandlerSpec) bootstrap.ChildInitializer
func HTTP3LocalControlStream(cfg http3.PipelineConfig) bootstrap.ChildInitializer
func HTTP3RemoteControlStream(cfg http3.PipelineConfig) bootstrap.ChildInitializer
func HTTP3RequestStream(cfg http3.PipelineConfig) bootstrap.ChildInitializer
func Initializer(specs ...HandlerSpec) bootstrap.ChildInitializer
func LengthFieldFrames(cfg LengthFieldConfig, app ...HandlerSpec) bootstrap.ChildInitializer
func LineFrames(cfg LineConfig, app ...HandlerSpec) bootstrap.ChildInitializer
func MQTTFrames(cfg MQTTConfig, app ...HandlerSpec) bootstrap.ChildInitializer
func WebSocketServer(cfg WebSocketServerConfig, app ...HandlerSpec) bootstrap.ChildInitializer
type HTTP1Config struct{ ... }
type HTTP2Config struct{ ... }
type HandlerFactory func() (channel.Handler, error)
type HandlerSpec struct{ ... }
    func Use(name string, handler channel.Handler) HandlerSpec
    func UseFactory(name string, factory HandlerFactory) HandlerSpec
type LengthFieldConfig struct{ ... }
type LineConfig struct{ ... }
type MQTTConfig struct{ ... }
type WebSocketServerConfig struct{ ... }
```
