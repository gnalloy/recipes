# recipes

Reusable Gnalloy pipeline assembly recipes for TCP, HTTP/1, HTTP/2, HTTP/3, WebSocket, and MQTT.

This repository is part of the Gnalloy modular networking stack. The default branch is `dev`; no release tag is created during bootstrap.

## Install

```bash
go get gnalloy.org/recipes@dev
```

## Module Boundary

- Module path: `gnalloy.org/recipes`
- Responsibility: Reusable Gnalloy pipeline assembly recipes for TCP, HTTP/1, HTTP/2, HTTP/3, WebSocket, and MQTT
- Core dependency: `gnalloy.org/gnalloy` when this module uses Gnalloy buffers, channels, event loops, or bootstrap contracts.

## Gnalloy Dependencies

- `gnalloy.org/gnalloy`
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`

## Development

```bash
go test ./... -count=1
go vet ./...
go test ./... -run '^$' -bench . -benchmem -benchtime=100ms -count=1
```

For multi-repository development, use the workspace at `G:\opensource\gnalloy\go.work`. For standalone verification, set `GOWORK=off`.

## License

Apache-2.0.
