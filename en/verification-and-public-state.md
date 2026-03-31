# Verification and Public State

This page explains how finalized projects move into verified public state and which chain inputs external platforms commonly rely on.

## 1. Finalize completes the launch transition

A project is not truly public just because it was created. It becomes public in the platform sense when finalize has completed and the token has entered its standardized market state.

## 2. The backend watches finalized projects

Backend watchers scan finalized projects and enqueue their tokens for source verification. Verification is therefore part of the launch pipeline rather than a disconnected manual step.

## 3. source-verify resolves the correct profile

The verification service supports the standard token path and can also resolve verification metadata from compatible custom token cores. It determines:

- source path
- contract name
- matching build info

before submitting a verification request.

## 4. Public state is built from on-chain inputs

The platform cannot force third-party scanners to refresh instantly, but it can make sure the chain state it produces is consistent. The important inputs include:

- source verified
- owner closed out
- presale address cleared
- key launch permissions locked
- LP burned
- trading enabled

## 5. Why this matters

If a platform stops at deployment and fundraising, public status becomes an afterthought. SPLY treats verified, market-ready state as part of the product flow.

## 6. Interpreting third-party displays

External platforms may cache differently or interpret inputs differently. SPLY’s job is to keep the on-chain state path and verification path consistent so those platforms have stable inputs to read.
