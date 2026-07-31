# Proxy Checker

Go worker for validating HTTP, HTTPS, SOCKS4, and SOCKS5 proxies.

## Overview

Proxy Checker consumes versioned check jobs, tests a proxy through one or more IP Judge nodes, and publishes normalized results.
Status: foundation planning. The archived Python checker remains historical reference material; v2 will use explicit contracts and SSRF-safe networking.

## Architecture

~~~text
AMQP queue
    |
    v
Checker worker -> protocol adapter
    |
    v
Regional IP Judge nodes
    |
    v
Versioned check result
~~~

The shared message and API shapes are owned by [proxy-contracts](https://github.com/ichinya/proxy-contracts).

## Features

Planned capabilities:

- HTTP proxy checks
- HTTPS CONNECT checks
- SOCKS4 and SOCKS5 checks
- Multiple RU/EU/other judge nodes
- LavinMQ and RabbitMQ worker mode
- Connection, response, and total latency measurements
- Proxy anonymity signals
- SSRF protection for private, loopback, and metadata networks

## Installation

No runnable release is available yet. Clone the repository to review the specifications and follow the v0.1 issues for the initial implementation.

~~~shell
git clone https://github.com/ichinya/proxy-checker.git
cd proxy-checker
~~~

## Docker

A production container image is planned for v0.1 where applicable. Until an image and digest are published, there is no supported container invocation.

## Configuration

Jobs and results follow proxy-contracts. Network destinations are validated before dialing and again after DNS resolution or redirects.

## Environment variables

| Variable | Purpose |
| --- | --- |
| `AMQP_URL` | AMQP broker connection string |
| `IP_JUDGE_URLS` | Comma-separated judge endpoints |
| `CHECK_TIMEOUT` | Maximum duration of one check |
| `WORKER_CONCURRENCY` | Maximum concurrent checks |
| `LOG_LEVEL` | Structured log level |

Names and defaults are proposed and may change before v0.1. Never commit production secrets.

## Development

Target runtime: Go.

1. Choose an open roadmap issue and confirm its acceptance criteria.
2. Keep contracts and examples versioned; coordinate cross-repository changes explicitly.
3. Add tests for behavior changes and update documentation in the same pull request.
4. Run the repository-specific checks documented by the implementation once they exist.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the common workflow and [SECURITY.md](SECURITY.md) for private vulnerability reporting.

## Roadmap

- **v0.1 Foundation:** repository structure, documentation, Docker/CI foundations, and base contracts.
- **v0.2 MVP:** collector -> scheduler -> MQ -> checker -> judge -> database -> site working cycle.
- **v1.0 Production:** multi-region judges, scoring, API, billing, monitoring, and high availability.

Track delivery in the [repository milestones](https://github.com/ichinya/proxy-checker/milestones) and [issues](https://github.com/ichinya/proxy-checker/issues).

## Related projects

- [ip-judge](https://github.com/ichinya/ip-judge)
- [proxy-contracts](https://github.com/ichinya/proxy-contracts)
- [proxy-scheduler](https://github.com/ichinya/proxy-scheduler)
- [proxy-stack](https://github.com/ichinya/proxy-stack)

## License

MIT License
