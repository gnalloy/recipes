# API Reference

[简体中文](api.zh-CN.md) | [Docs Index](README.md)

This inventory is generated from `go doc -short` for the packages in this repository. It is a quick public-surface map; source files and tests remain the authority for exact semantics.

## Packages

### `gnalloy.org/recipes`

Package name: `recipes`

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
