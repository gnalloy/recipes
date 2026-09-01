# recipes

[简体中文](README.zh-CN.md) | [Documentation](docs/README.md)

Reusable Gnalloy pipeline assembly recipes for TCP, HTTP/1, HTTP/2, HTTP/3, WebSocket, and MQTT.

This module provides reusable assembly recipes. Recipes combine core, codec, handler, and transport modules into common pipelines while keeping the underlying modules independently usable.

## Status

- Import path: `gnalloy.org/recipes`
- Repository: `github.com/gnalloy/recipes`
- Default branch: `dev`
- Preview install: `go get gnalloy.org/recipes@dev`
- License: Apache-2.0

## Install
```bash
go get gnalloy.org/recipes@dev
go doc gnalloy.org/recipes
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
```

## Documentation
- [Overview](docs/overview.md) ([中文](docs/overview.zh-CN.md))
- [Usage](docs/usage.md) ([中文](docs/usage.zh-CN.md))
- [Examples](docs/examples.md) ([中文](docs/examples.zh-CN.md))
- [Configuration](docs/configuration.md) ([中文](docs/configuration.zh-CN.md))
- [Testing and Performance](docs/testing.md) ([中文](docs/testing.zh-CN.md))
- [API Reference](docs/api.md) ([中文](docs/api.zh-CN.md))
- [Notes and Caveats](docs/notes.md) ([中文](docs/notes.zh-CN.md))
- [ADR-001 Module Boundary](docs/decisions/0001-module-boundary.md) ([中文](docs/decisions/0001-module-boundary.zh-CN.md))

## Module Boundary

This repository owns: Reusable Gnalloy pipeline assembly recipes for TCP, HTTP/1, HTTP/2, HTTP/3, WebSocket, and MQTT.

It does not absorb neighboring module responsibilities. Core primitives stay in `gnalloy.org/gnalloy`; protocol codecs, transports, handlers, resolvers, examples, and benchmarks stay in their own repositories.

## Packages
- `gnalloy.org/recipes` (`recipes`)

## Gnalloy Dependencies
- `gnalloy.org/gnalloy`
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`

## Common Integration Pattern
- Configuration is passed through explicit constructors and option structs rather than package-level mutable state.
- Keep hot-path defaults conservative, bounded, and allocation-aware.
- Raw IP paths normally require administrative privileges or `CAP_NET_RAW` on systems that support raw sockets.

## Current Public Entry Points

The generated API reference lists the full public surface. Common constructors or option types currently include:
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

## Verification

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
GOWORK=off GOTOOLCHAIN=local go vet ./...
GOWORK=off GOTOOLCHAIN=local go test ./... -run '^$' -bench . -benchmem -count=1
```

For pressure tests, assemble this module with the relevant transport, codec, and handler stack and run the scenario from `gnalloy.org/benchmarks` or `gnalloy.org/examples`. Keep host, operating system, payload, concurrency, warmup, and repetitions in the report.

## Caveats
- This repository is intentionally narrow. Cross-module behavior should be assembled in applications, recipes, examples, or benchmark harnesses.
- Public APIs should remain Go-native and explicit; avoid runtime scanning, hidden global registries, and reflection-heavy behavior in hot paths.
- Treat network input as untrusted. Configure parser limits and return typed errors instead of panics.
- Keep benchmark claims tied to a concrete host, operating system, protocol, payload, concurrency, warmup, and repetition count.
