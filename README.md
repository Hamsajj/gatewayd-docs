# Documentation

The initial docs structure is detailed in [this comment](https://github.com/gatewayd-io/docs/issues/1#issuecomment-1442331491) and is as follows. This will be updated over time as the docs is written and shaped.

- Getting started
  - [x] [Welcome](docs/getting-started/welcome.md)
  - [x] [Installation](docs/getting-started/installation.md)
  - [x] [Running GatewayD](docs/getting-started/running-gatewayd.md)
  - [ ] [Resources](docs/getting-started/resources.md)
- Using GatewayD
  - [x] [Configuration](docs/using-gatewayd/configuration.md)
    - [x] [Global configuration](docs/using-gatewayd/configuration.md#global-configuration)
      - [x] [Loggers](docs/using-gatewayd/global-configuration/loggers.md)
      - [x] [Metrics](docs/using-gatewayd/global-configuration/metrics.md)
      - [x] [Clients](docs/using-gatewayd/global-configuration/clients.md)
      - [x] [Pools](docs/using-gatewayd/global-configuration/pools.md)
      - [x] [Proxies](docs/using-gatewayd/global-configuration/proxies.md)
      - [x] [Servers](docs/using-gatewayd/global-configuration/servers.md)
      - [x] [API](docs/using-gatewayd/global-configuration/api.md)
    - [x] [Plugins configuration](docs/using-gatewayd/configuration.md#plugins-configuration)
      - [x] [General configuration](docs/using-gatewayd/plugins-configuration/general-configurations.md)
      - [x] [Plugins configuration](docs/using-gatewayd/plugins-configuration/plugins-configuration.md)
    - [x] [Environment variables](docs/using-gatewayd/configuration.md#environment-variables)
    - [x] [Runtime configuration](docs/using-gatewayd/configuration.md#runtime-configuration)
  - [x] [CLI](docs/using-gatewayd/CLI.md)
  - [x] [Servers](docs/using-gatewayd/servers.md)
  - [x] [Clients](docs/using-gatewayd/clients.md)
  - [x] [Pools](docs/using-gatewayd/pools.md)
  - [x] [Proxies](docs/using-gatewayd/proxies.md)
  - [x] [Observability](docs/using-gatewayd/observability.md)
  - [x] [API](docs/using-gatewayd/API.md)
  - [x] [Connection lifecycle](docs/using-gatewayd/connection-lifecycle.md)
  - [x] [Protocols](docs/using-gatewayd/protocols.md)
- Using plugins
  - [x] [Plugins](docs/using-plugins/plugins.md)
  - [x] [Hooks](docs/using-plugins/hooks.md)
  - [x] [Plugin registry](docs/using-plugins/plugin-registry.md)
  - [x] [Hook registry](docs/using-plugins/hook-registry.md)
  - [x] [Plugin types](docs/using-plugins/plugin-types.md)
  - [x] [Proposals](docs/using-plugins/proposals.md)
- Developing plugins
  - [x] [Plugin developers guide](docs/developing-plugins/plugin-developers-guide.md)
  - [x] [SDK](docs/developing-plugins/sdk-reference.md)
  - [x] [gRPC API reference](docs/developing-plugins/grpc-api-reference.md)
  - [x] [Template projects](docs/developing-plugins/template-projects.md)
- Plugins
  - [x] [gatewayd-plugin-cache](docs/plugins/gatewayd-plugin-cache.md)
- GatewayD versus (move to the blog?)
  - [ ] Bouncers (`PgBouncer`, `PgPool-II` and `pgcat`)
  - [ ] `MaxScale`
  - [ ] `ProxySQL`
  - [ ] `Acra`
  - [ ] `Stargate`
  - [ ] `Heimdall Data`
  - [ ] `Bytebase`
  - [ ] `Airbyte`
  - [ ] `Arana`
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
  - [x] [Telemetry and usage report](docs/miscellaneous/telemetry-and-usage-report.md)
  - [ ] Error reporting
  - [ ] Release notes
  - [ ] [Glossary](docs/miscellaneous/glossary.md)

## Running the docs locally

The docs are built using [Jekyll](https://jekyllrb.com/) and the [just-the-docs](https://just-the-docs.github.io/just-the-docs/) theme. To run the docs locally, you need to have Git and Ruby installed. Then, install Jekyll and `bundler`:

```bash
gem install jekyll bundler
```

Then, install the dependencies:

```bash
bundle install
```

Finally, run the docs:

```bash
bundle exec jekyll serve
```

If you want to clean the build directory, run:

```bash
bundle exec jekyll clean
```
