# bonobo

**Flow-based DAST engine for OpenAPI and GraphQL APIs**

Bonobo is an open-source **Dynamic Application Security Testing (DAST)** engine designed specifically for **API-first systems**.  
Instead of testing endpoints in isolation, Bonobo executes **stateful, ordered flows** that reflect real-world API usage patterns.

It supports **OpenAPI (REST)** and **GraphQL** natively and is built around a **modular, plugin-driven architecture** implemented in C#.

---

## Why Bonobo?

Traditional DAST tools treat APIs as a collection of independent endpoints.  
Bonobo takes a different approach:

- APIs are **stateful**
- Endpoints are **connected**
- Security issues often emerge **across steps**, not in single requests

Bonobo models APIs as **execution paths** and validates them through **complete resource lifecycles**:

```
Create → Read → Update → Delete
```

This enables more realistic security testing, better coverage, and fewer false positives.

---

## Core Concepts

### Flow-based execution
Tests are executed as **flows**, not single calls.  
A flow represents a meaningful business or technical scenario.

### Step orchestration
Each flow is composed of ordered steps with:
- Data dependencies
- Context propagation
- Dynamic variable resolution

### API lifecycle awareness
Bonobo understands the lifecycle of API resources and validates:
- Authorization boundaries
- State transitions
- Inconsistent or unsafe behaviors

### Plugin-first architecture
Everything is extensible:
- Protocols
- Auth strategies
- Assertions
- Reporters

---

## Supported APIs

### OpenAPI (REST)
- Path-based execution
- Parameter and schema awareness
- Contract-driven flows

### GraphQL
- Query and mutation flows
- Resolver-level execution paths
- Graph traversal and dependency handling

---

## Architecture Overview

```
bonobo
 ├─ plugins
 ├─ cli
 └─ docs
```

Bonobo is designed as an **engine**, not a monolithic scanner.

---

## CLI Usage

Bonobo ships with a lightweight CLI to execute flows locally or in CI/CD pipelines.

### OpenAPI flow execution

```bash
bonobo run   --openapi ./openapi.yaml   --base-url https://api.example.com
```

### GraphQL execution

```bash
bonobo run   --graphql https://api.example.com/graphql   --schema ./schema.graphql
```

---

## Common Flags

| Flag | Description |
|-----|------------|
| `--openapi <file>` | Path to OpenAPI specification |
| `--graphql <url>` | GraphQL endpoint |
| `--schema <file>` | GraphQL schema file |
| `--base-url <url>` | Base API URL |
| `--auth <plugin>` | Authentication plugin |
| `--flow <name>` | Execute a specific flow |
| `--steps <list>` | Execute selected steps |
| `--env <file>` | Environment variables |
| `--report <format>` | Output report format |
| `--fail-on <level>` | Exit on severity threshold |
| `--dry-run` | Validate flows without execution |
| `--verbose` | Enable verbose output |

---

## Example Flow (Conceptual)

```
UserRegistrationFlow
 ├─ CreateUser
 ├─ AuthenticateUser
 ├─ UpdateProfile
 └─ DeleteUser
```

Each step can:
- Consume output from previous steps
- Assert security conditions
- Mutate execution context

---

## Use Cases

- API security testing in CI/CD
- Stateful authorization validation
- Regression testing for API changes
- Security testing for GraphQL resolvers
- OpenAPI contract validation through execution

---

## License

Bonobo is released under the **Mozilla Public License 2.0 (MPL 2.0)**.

- The core engine is open-source
- Modifications to MPL-licensed files must remain open
- Proprietary extensions, UIs and enterprise features are allowed

This licensing model enables an **open-core strategy** while protecting community contributions.

See the `LICENSE` file for details.

---

## Roadmap

- Advanced GraphQL graph traversal
- Visual flow editor (commercial)
- Web UI and dashboards (commercial)
- Enterprise auth and policy plugins
- SaaS execution mode

---

## Contributing

Contributions are welcome.

Please:
- Follow the existing architecture
- Keep plugins isolated and modular
- Add tests for new flows or assertions

A formal contribution guide will be added soon.

---

## Philosophy

Bonobo is not a scanner.  
It is an **API execution engine with a security mindset**.

Security emerges from understanding **how APIs are actually used** — not from isolated requests.
