# Documentation

The initial docs structure is detailed in [this comment](https://github.com/gatewayd-io/docs/issues/1#issuecomment-1442331491) and is as follows. This will be updated over time as the docs is written and shaped.

- Getting started
  - [x] [Welcome](pages/getting-started/01-welcome.md)
  - [x] [Installation](pages/getting-started/02-installation.md)
  - [x] [Running GatewayD](pages/getting-started/03-running-gatewayd.md)
  - [x] [Observability](pages/getting-started/04-observability.md)
  - [ ] [Resources](pages/getting-started/05-resources.md)
- Using GatewayD
  - [ ] [Configuration](pages/using-gatewayd/01-configuration.md)
    - [ ] Global Configuration
      - [x] [Loggers](pages/using-gatewayd/01-configuration/01-global-configuration/01-loggers.md)
      - [x] [Metrics](pages/using-gatewayd/01-configuration/01-global-configuration/02-metrics.md)
      - [x] [Clients](pages/using-gatewayd/01-configuration/01-global-configuration/03-clients.md)
      - [x] [Pools](pages/using-gatewayd/01-configuration/01-global-configuration/04-pools.md)
      - [x] [Proxies](pages/using-gatewayd/01-configuration/01-global-configuration/05-proxies.md)
      - [x] [Servers](pages/using-gatewayd/01-configuration/01-global-configuration/06-servers.md)
      - [ ] [API](pages/using-gatewayd/01-configuration/01-global-configuration/07-api.md)
    - Plugins
    - Environment variables
    - Runtime configuration
  - [ ] CLI
  - [ ] Servers
  - [ ] Clients
  - [ ] Pools
  - [ ] Proxies
    - L4 transparent proxy
    - Health check
  - [ ] Observability
    - Loggers
    - Metrics
    - Traces
  - [ ] API
    - gRPC
    - HTTP
  - [ ] Connection lifecycle
  - [ ] Protocols
- Using plugins
  - [ ] Plugins
    - Policies
      - Verification
      - Compatibility
      - Acceptance
    - Reload on crash
    - Health check
    - Metrics merger
    - Command-line arguments
    - Environment variables
    - Checksum verification
  - [ ] Hooks
    - Types (traffic and notification)
    - Timeout
  - [ ] Plugin registry
  - [ ] Hook registry
  - [ ] Plugin types
    - Built-in plugins
    - Community plugins
    - Enterprise plugins
  - [ ] Proposals
- Developing plugins
  - [ ] Plugin lifecycle
  - [ ] SDK reference
  - [ ] gRPC API reference
  - [ ] Template projects (Go and Python)
- GatewayD versus
  - [ ] MaxScale
  - [ ] ProxySQL
  - [ ] Acra
  - [ ] Stargate
  - [ ] Heimdall Data
  - [ ] Bytebase
  - [ ] Airbyte
  - [ ] Arana
  - [ ] Bouncers (PgBouncer, PgPool-II and pgcat)
- Community
  - [ ] Learning
  - [ ] Contributing
    - GatewayD public roadmap
    - Plugins public roadmap
    - Public proposals
  - [ ] Forum
  - [ ] Chat
  - [ ] Social accounts
  - [ ] Code of conduct
  - [ ] Test server
- Misc
  - [ ] Telemetry and usage report
  - [ ] Error reporting
  - [ ] Release notes
  - [ ] Glossary
