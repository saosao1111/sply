# Architecture and Components

## System layers

SPLY can be understood as a three-layer system:

## 1. On-chain protocol layer

This layer handles project creation, custody, fundraising state, template routing, market transition, and permission closure. The main contracts are:

- `LaunchFactory`
- `TemplateFactory`
- `FactoryAdmin`
- `Presale`
- `Vault`
- token cores
- deployers

## 2. Backend service layer

The backend indexes projects, serves APIs, runs automated verification, maintains admin review data, and turns chain state into public-facing responses.

## 3. Frontend product layer

The frontend exposes the home page, create flow, templates page, developer page, project pages, token pages, and admin review flow.

## Contract roles

## LaunchFactory

`LaunchFactory` is the project-level factory. It is responsible for:

- creating token, vault, and presale
- running project setup
- attaching token hooks
- handling standard token and custom core deployment paths
- managing salt pools for standard and custom token cores

## TemplateFactory

`TemplateFactory` routes template launches. It decides whether the selected template is:

- a built-in template
- an approved developer template
- a platform custom core path
- a self-deployed custom core path

## FactoryAdmin

`FactoryAdmin` governs the developer template registry:

- registering templates
- enabling and disabling templates
- storing capability flags and schema policy data
- allowing emergency shutdown of eligible projects

## Presale

`Presale` is the fundraising state machine:

- participation
- fundraising progress
- finalize
- refund and vote-related transitions when configured

## Vault

`Vault` is the custody boundary for presale funds. Its purpose is to keep fundraising assets outside of arbitrary template logic and tied to the presale state model.

## Token core

Token cores implement token behavior:

- transfers
- tax behavior
- permission gates
- market state hooks

Built-in paths and developer template paths may use different token cores, but they still need to fit the platform lifecycle.

## Ownership split

The current live architecture separates control:

- `Factory` and `TemplateFactory` stay under Safe ownership
- `FactoryAdmin` can be operated through a more flexible operator wallet

This split keeps the core launch path under stronger control while allowing faster template review and template registration operations.
