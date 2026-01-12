## About

Backend/platform engineer. I build distributed systems and internal tooling.

**Current focus:**
- Microservices with event sourcing (Marten/PostgreSQL)
- Developer platforms with enforced standards via tooling
- Auth infrastructure (JWT/OAuth2/Keycloak)
- Observability stack (OpenTelemetry, <5ms overhead)

Stack: .NET 10, PostgreSQL, Docker, Kubernetes, gRPC, Redis/Aerospike

See [stack.md](./stack.md) for full list.

---

## Design principles

1. **Architecture is a product** — Internal platforms need the same discipline as customer-facing products
2. **Observability is non-negotiable** — Metrics/traces/logs designed upfront, not added later
3. **Security > convenience** — mTLS, RBAC, policy enforcement first. Shortcuts never.
4. **Automate enforcement** — CI/CD gates and linters beat documentation

---

## Projects

### [RyzeSpace](https://github.com/ryzespace/ryzespace)
Multi-service platform for microservices orchestration and peer-to-peer resource sharing.

**Core platform:**
- Event driven microservices (Wolverine message bus)
- Event sourcing with Marten (PostgreSQL)
- Centralized auth via Keycloak (multi-tenant JWT)
- OpenTelemetry for distributed tracing
- K8s deployment with zero downtime rollouts

**Resource sharing system:**
- Peer to peer computing resource rental (containers, RAM disks, custom workloads)
- Lightweight agent with namespace/VM/container isolation
- Resource level access control and encrypted communication
- Real-time monitoring and remote execution

**Use cases:**
- Gaming servers hosted from user machines
- Company infrastructure scaling with distributed resources
- RAM disks and temporary test instances
- Sandboxed dev environments

**Stack:** .NET 10, PostgreSQL, Marten, Wolverine, Keycloak, Docker, K8s, gRPC, Linux namespaces

[![Discussions](https://img.shields.io/badge/Discussions-ryzespace-2F5D50?style=flat-square)](https://github.com/orgs/ryzespace/discussions)

---

### [AuthKit](https://github.com/AuthKits/AuthKit.Server)
Authentication and authorization framework for .NET microservices. Integrates with Keycloak for identity management and provides SDK-level access control.

**Architecture:**
- Keycloak integration for developer identity and OAuth2 flows
- SDK token issuance with scoped permissions
- Multi-tenant JWT validation with configurable policies
- Plugin architecture for custom identity providers

**Use case:** Centralized auth microservice for RyzeSpace SDK ecosystem—ensures only authorized developers can access SDK methods with auditable token-based verification.

**Stack:** .NET 10, ASP.NET Core, Keycloak, JWT/OAuth2

![Issues](https://img.shields.io/github/issues/AuthKits/AuthKit.Server?style=flat-square&labelColor=2F5D50&color=2F5D50) ![PRs](https://img.shields.io/github/issues-pr/AuthKits/AuthKit.Server?style=flat-square&labelColor=2F5D50&color=2F5D50)

---

### [ModularityKit](https://github.com/rian-be/ModularityKit)
High performance framework for building modular .NET applications with clear separation of concerns and type safe inter module communication.

**Architecture:**
- Module system with plugin-style component loading
- Pipeline & middleware for composable processing chains
- Signal based event system for decoupled communication (type safe, no reflection at runtime)
- Precompiled execution paths for minimal overhead

**Problem it solves:** Large scale applications often become tightly coupled monoliths. ModularityKit enforces boundaries between modules while maintaining type safety and performance enables teams to work independently on features without stepping on each other.

**Use case:** Foundation for modular monoliths that can be extracted to microservices later without architectural rewrites.

**Stack:** .NET 10, DI

![Issues](https://img.shields.io/github/issues/rian-be/ModularityKit?style=flat-square&labelColor=2F5D50&color=2F5D50) ![PRs](https://img.shields.io/github/issues-pr/rian-be/ModularityKit?style=flat-square&labelColor=2F5D50&color=2F5D50)

---

## Architecture approach

**Vertical Slice Architecture + DDD:**
- Features organized by business capability, not technical layers
- Each slice owns its data access, validation, and business logic
- Bounded contexts define service boundaries
- Shared kernel kept minimal duplication over coupling

**Event-driven patterns:**
- CQRS when read/write models diverge
- Saga pattern for long-running workflows
- Outbox pattern for reliable event publishing
- Event sourcing for audit trails and temporal queries

**Technology choices:**
- **Marten + PostgreSQL** — Event sourcing, projections, and relational queries in one package
- **Wolverine** — Local message bus with native Marten integration, handles retries/outbox automatically
- **gRPC for service to service** — Type safety, better performance than REST, auto generated clients
- **Keycloak** — Standardized auth flows, reduces custom security code surface area

---

## Contact

- GitHub: [@rian-be](https://github.com/rian-be)
- Discord: `rian.be`

---

<p align="center" style="color:#2F5D50; font-size:0.9em;">
© 2026 • Rainbe
</p>