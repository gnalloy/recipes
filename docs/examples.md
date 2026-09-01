# Examples

[简体中文](examples.zh-CN.md) | [Docs Index](README.md)

## Example 1: Add the Module to an Application

```bash
mkdir gnalloy-app && cd gnalloy-app
go mod init example.com/gnalloy-app
go get gnalloy.org/recipes@dev
go doc gnalloy.org/recipes
```

## Example 2: Inspect Current Packages

The current source tree exposes these package import paths:
- `gnalloy.org/recipes`

Use `go doc` against the package that matches the behavior you need:

```bash
go doc gnalloy.org/recipes
```

Selected current exported entry points:
- `const HandlerNameHTTP1RequestDecoder = "http1-request-decoder" ...`
- `const HandlerNameMQTTFrameDecoder = "mqtt-frame-decoder" ...`
- `const HandlerNameByteBufEcho = "bytebuf-echo" ...`
- `const HandlerNameWebSocketHandshake = "websocket-handshake" ...`
- `var ErrInvalidRecipe = errors.New("gnalloy/recipes: invalid recipe")`
- `func Apply(ch channel.Channel, specs ...HandlerSpec) error`

## Example 3: Use Executable Tests as Behavioral Examples

Repository tests are executable examples of supported behavior. Start with the selected names below, then read the matching `_test.go` files for complete setup and assertions. See [Testing and Performance](testing.md) for the complete discovered list.

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -run Test -count=1
```

Selected current test, benchmark, fuzz, and example entry points:
- `TestHTTP1ServerRecipe`
- `TestHTTP2ConnectionRecipeInstallsPipeline`
- `TestInitializerRollsBackOnFactoryError`
- `TestLengthFieldFramesRoundTrip`
- `TestMQTTFramesRecipe`
- `TestWebSocketServerRecipeUpgrade`

## Example 4: Cross-Module Assembly

Direct Gnalloy dependencies for this module:
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`
- `gnalloy.org/gnalloy`

Assembly guidance:
- Use recipes as reusable assembly guidance for common Gnalloy stacks.
- Recipes should depend on public module contracts and should not hide production policy from applications.
- Validate each recipe with its own integration and pressure scenario before copying it into a service.

## Example 5: Pressure-Test Harness

For sustained load, wire this module into a scenario under `gnalloy.org/benchmarks` or a runnable client under `gnalloy.org/examples` when the module participates in network traffic. Record host, OS, CPU, Go version, protocol, payload, concurrency, warmup, repetitions, throughput, and p99 latency in the report.
