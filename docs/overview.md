# Overview

[简体中文](overview.zh-CN.md) | [Docs Index](README.md)

## Purpose

Reusable Gnalloy pipeline assembly recipes for TCP, HTTP/1, HTTP/2, HTTP/3, WebSocket, and MQTT.

This module provides reusable assembly recipes. Recipes combine core, codec, handler, and transport modules into common pipelines while keeping the underlying modules independently usable.

## Repository Identity

- Module path: `gnalloy.org/recipes`
- GitHub repository: `github.com/gnalloy/recipes`
- Default branch: `dev`
- License: Apache-2.0

## Package Map
- `gnalloy.org/recipes` (`recipes`)

## Direct Gnalloy Dependencies
- `gnalloy.org/gnalloy`
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`
- `gnalloy.org/codec-http3`
- `gnalloy.org/codec-mqtt`
- `gnalloy.org/codec-websocket`

## Direct Dependents in the Current Module Plan
- No repository in the current module plan depends on this module directly.

## Architecture Position

Gnalloy keeps the core small and dependency-light. This repository is a replaceable module around one responsibility, connected through explicit Go packages instead of runtime discovery.

## Compatibility

The public import path is `gnalloy.org/recipes`. Until the first stable tag is published, use `@dev` or an explicit pseudo-version selected by your dependency policy.
