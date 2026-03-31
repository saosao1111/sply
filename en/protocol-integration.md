# Protocol Integration

This page is for wallets, bots, terminals, indexers, and third-party data consumers.

## Network

- Network: `BNB Smart Chain Mainnet`
- Chain ID: `56`

See [Deployed Contract Addresses](./deployed-contract-addresses.md) for the current live addresses.

## Primary on-chain entry points

The most important contracts for integrations are:

- `LaunchFactory`
- `TemplateFactory`
- `FactoryAdmin`

These define where projects are created, how templates are routed, and which template set is official.

## Project-centric data model

Integrations should think in terms of project objects rather than raw token discovery. The stable model is:

- project id
- presale
- token
- vault
- pair

This is the same relationship the platform uses in its frontend and backend aggregation.

## Prefer platform APIs for public surfaces

If your goal is to display:

- project lists
- project detail pages
- token market views
- recent trade lists

it is usually better to start with SPLY’s APIs rather than rebuilding every view directly from chain events.

## When direct chain reads still matter

Direct reads are still appropriate when:

- you operate your own indexer
- you need final chain truth
- you build monitoring and alerting
- you validate project status independently

## Integration priorities

The most useful checks are:

- whether a project came from the official factory
- whether a template came from the official registry
- whether the project has finalized
- whether a pair exists
- whether the token has entered market state
