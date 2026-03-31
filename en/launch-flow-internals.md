# Launch Flow Internals

This page describes the SPLY launch flow from the perspective of protocol execution.

## 1. The frontend encodes a launch request

The create page encodes the project configuration and template parameters and submits the request through the factory path.

## 2. TemplateFactory performs template routing

`TemplateFactory` determines which launch route applies:

- built-in template path
- approved developer template path
- platform-managed custom core path
- developer self-deployed core path

The platform turns template choice into the correct contract execution path.

## 3. LaunchFactory creates the project components

`LaunchFactory` creates and wires together:

- token
- vault
- presale

Depending on the template route, token deployment can use the standard token deployer, the platform custom core `CREATE2` path, or a validated developer-supplied core.

## 4. Project setup aligns supply and fundraising logic

During setup, `LaunchFactory` transfers the required project token supply into the presale path and links the project contracts together.

The purpose is not just initialization. It is to make the fundraising formula and the later finalize path line up.

## 5. Token hooks connect the token core to platform lifecycle

The platform calls token-side hooks such as presale and market-related configuration hooks so the token core is attached to the platform lifecycle instead of floating outside it.

## 6. Participation advances the presale

When a user participates:

- BNB is moved into custody
- presale progress advances
- token distribution logic is applied through the project formula

## 7. Finalize moves the project into market state

Finalize is the critical transition. It coordinates:

- fee handling
- LP creation
- pair discovery
- market configuration
- LP burn
- trading enablement
- lock actions
- temporary permission closure
- presale address cleanup

## 8. Backend watchers continue the pipeline

Once finalized, backend watchers enqueue the token for verification and keep the public surfaces in sync with the project’s new phase.

## Why the internal flow matters

Without this structure, templates would effectively become independent launch systems. SPLY is designed so templates extend token logic while the platform keeps control over the fundraising and market transition lifecycle.
