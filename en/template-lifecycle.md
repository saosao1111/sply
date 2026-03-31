# Template Lifecycle

This page explains how a developer template moves from submission to becoming a public platform template.

## 1. Development

The developer implements a deployer and token core path that satisfy platform requirements.

## 2. Submission

The template is submitted through the developer submission flow and enters the review queue.

## 3. Review

The admin side reviews:

- the mechanism
- interface completeness
- parameter structure
- obvious permission and lifecycle risks

## 4. Registration

Approved templates are registered through `FactoryAdmin`, which stores the template in the on-chain registry with policy metadata.

## 5. Public listing

Once registered, the frontend reads the template from the on-chain template set and exposes it to project owners.

## 6. Live use

Project owners can now select the template, provide its parameter set, and launch through the platform.

## 7. Ongoing governance

The platform can still manage whether the template remains enabled, which prevents the public template set from becoming unmanaged over time.
