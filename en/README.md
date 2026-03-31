# Welcome to SPLY

SPLY is a template-driven launch platform on BNB Smart Chain. It is not just a token deployment page and not just a loose set of contracts. It is a coordinated launch system that connects project creation, fundraising, custody, market opening, verification, project presentation, and template approval into one product flow.

This documentation is rebuilt from the current platform structure and is intended for four groups:

- token teams that want to launch through a standardized presale flow
- mechanism developers that want to make their own token logic available as public platform templates
- participants and traders that want consistent project and token pages
- wallets, bots, terminals, indexers, and data teams that need stable protocol and API surfaces

## What SPLY is

SPLY does not try to solve only one action such as “deploy a token”. Its core value is to standardize the full launch path:

- token deployment
- presale custody
- fundraising state transitions
- liquidity creation
- trading enablement
- permission shutdown
- source verification
- public-facing project and token state

This lets the platform support multiple mechanisms without turning every template into its own isolated launch process.

## What SPLY solves

Launching a token on BSC is easy. Launching through a repeatable, auditable, extensible platform is much harder:

- teams often handle token deployment, fundraising, LP creation, permission shutdown, and verification through separate tools
- once multiple mechanisms are introduced, platform standards can drift
- public scanner inputs depend on whether the on-chain finalize path is consistent
- opening developer templates without a registration and review layer turns the platform into an uncontrolled template market

SPLY exists to solve those problems by turning launch behavior into a platform standard instead of a per-template improvisation.

## Core strengths

## 1. One launch standard across different mechanisms

SPLY keeps the launch process coordinated through distinct protocol roles:

- `LaunchFactory`
- `TemplateFactory`
- `Presale`
- `Vault`
- token cores
- `FactoryAdmin`

Teams may choose different token logic, but they do not leave the platform launch system when they do so.

## 2. Fund custody is separated from token logic

Presale funds live in `Vault`, fundraising state lives in `Presale`, and token behavior lives in token cores. This separation matters because templates can extend token behavior without directly taking control over platform-raised funds.

## 3. Deterministic deployment is a platform capability

SPLY treats `CREATE2` and salt management as a platform-level capability. The platform maintains dedicated salt pools per token core type so deterministic deployment is not limited to one built-in token path.

## 4. Market opening and state closure are part of finalize

Finalize is not just a bookkeeping step. It is the path that moves a project from fundraising into a standard public market state by handling:

- platform fee processing
- LP creation
- pair discovery
- market configuration
- LP burn
- trading enablement
- permission closure
- verification enqueueing

## 5. Developer templates are first-class platform templates

Approved developer templates are not treated as an external plugin layer. Once reviewed and registered, they become part of the public template set and continue to use the platform launch process, address planning model, and verification flow.

## 6. Frontend, backend, and on-chain state are connected

SPLY includes:

- a public launch interface
- project pages
- token pages
- a developer submission surface
- an admin review surface
- backend APIs
- indexing and verification services

This makes it a product system, not just a contract package.

## Documentation map

- [Overview](./platform-overview.md)
- [Why SPLY](./why-sply.md)
- [How Launching Works](./how-launching-works.md)
- [Architecture and Components](./architecture-and-components.md)
- [Launch Flow Internals](./launch-flow-internals.md)
- [Project Owner Guide](./project-owner-guide.md)
- [Developer Template Guide](./developer-template-guide.md)
- [Template Lifecycle](./template-lifecycle.md)
- [Protocol Integration](./protocol-integration.md)
- [Verification and Public State](./verification-and-public-state.md)
- [Deployed Contract Addresses](./deployed-contract-addresses.md)
- [API Reference](./api-reference.md)
- [Brand, Community, and Contact](./brand-and-community.md)
