# Developer Template Guide

This page explains how developers can bring new token behavior into SPLY and turn their mechanism into a public platform template.

## What a developer template is

A developer template is not an isolated token launcher living outside the platform. It is a reviewed extension that becomes part of the public template set and still follows platform launch rules.

## What a template includes

A template usually includes:

- a deployer
- a token core or token core deployment path

The deployer is responsible for decoding parameters, producing the token core, and exposing the hooks that the platform expects.

## Submission path

Developers submit:

- deployer information
- template name and description
- parameter structure
- review notes and supporting materials

Submission enters a review queue first. It does not become public immediately.

## Review and registration

When a template is approved, the admin side registers it through `FactoryAdmin`. Once registered:

- it receives a template id
- it becomes available in the public template list
- project owners can select it from the create page

## Required token-side hooks

Custom token cores must fit the platform lifecycle. That means they must support the hooks the platform relies on during launch and finalize, including:

- `setPresale`
- `setTaxStrategy`
- `setMarketConfig`
- `enableTrading`
- `lockAfterFinalize`
- `renounceByPresale`
- `clearPresale`

## Why the platform imposes those constraints

Because SPLY does not let templates take over fundraising and settlement responsibilities. Templates can extend token behavior, but they still need to cooperate with:

- platform custody
- presale state
- finalize state closure
- source verification

## Platform custom core support

The current architecture also supports developer templates entering the platform-managed `CREATE2` path, which means developer templates can use the same address-planning and verification model as official platform paths when they satisfy the required interfaces.

## Design recommendations

- keep the deployer focused on deployment and initialization
- keep custody logic out of custom token code
- avoid hidden mint, blacklist, or finalize-bypass logic
- define template parameters explicitly through `abi.decode`
- design the token core to be verifiable and reviewable
