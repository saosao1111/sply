# How Launching Works

This page explains the launch process from a product perspective. For the deeper call chain, see [Launch Flow Internals](./launch-flow-internals.md).

## 1. A team creates a project

On the create page, a team submits:

- token name and symbol
- total supply
- presale price
- soft cap and hard cap
- per-transaction and per-wallet limits
- end time
- logo, description, and links
- a selected template

## 2. The platform creates project components

The project is created through the factory system, which coordinates:

- token
- vault
- presale

## 3. Participants join the presale

Users contribute BNB to the presale path. Funds are held in custody and the presale state advances according to platform rules.

## 4. The project reaches finalize

When launch conditions are met, the finalize path handles the market transition:

- platform fee handling
- LP creation
- pair discovery
- market configuration
- LP burn
- trading enablement
- permission shutdown

## 5. The token moves into the public market phase

Once finalize is complete, the token page becomes the primary market-facing page with market data, liquidity data, and trade history.

## 6. Verification and public state follow

The backend verification flow then picks up finalized tokens and pushes them into the source verification pipeline.

## Why this matters

The key idea is that projects do not leave the platform at the moment they are created. They stay inside a coordinated lifecycle until they reach a standardized public market state.
