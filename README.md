# Proxy Checker

High performance proxy validation worker written in Go.

## Overview

Proxy Checker validates HTTP, HTTPS and SOCKS proxy endpoints using configurable IP Judge services.

## Features

- HTTP proxy checks
- HTTPS CONNECT support
- SOCKS4/SOCKS5 support
- Latency measurement
- Exit IP detection
- Queue worker mode
- Docker support

## Architecture

```
Scheduler -> Queue -> Proxy Checker -> IP Judge
```

## Development

Built with Go.

## License

MIT
