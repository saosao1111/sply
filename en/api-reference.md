# API Reference

This page lists the platform’s main public and admin APIs and describes what each route is for.

## Public APIs

## `GET /api/projects`

Purpose:

- return the public project list
- used by the home page and project listing views

## `GET /api/project/:id`

Purpose:

- return a single project view
- used by the project detail page

## `GET /api/token/:addr`

Purpose:

- return token-facing metadata linked to a platform project

## `GET /api/token-market/:address`

Purpose:

- return market-facing token data

## `GET /api/token-liquidity/:address`

Purpose:

- return liquidity-facing token data

## `GET /api/token-trades/:address`

Purpose:

- return recent trade history

## Content APIs

## `POST /api/upload`

Purpose:

- upload project assets such as logos

## `POST /api/save-metadata`

Purpose:

- save public project metadata

## Developer Submission APIs

## `POST /api/dev-submit`

Purpose:

- submit a developer template for review

## `GET /api/dev-submissions`

Purpose:

- list template submissions

## Admin APIs

## `GET /api/admin/nonce`

Purpose:

- issue an admin login nonce

## `POST /api/admin/login`

Purpose:

- create an admin session

## `POST /api/admin/logout`

Purpose:

- end the admin session

## `GET /api/admin/stats`

Purpose:

- return operator-facing statistics

## `POST /api/admin/dev-review`

Purpose:

- approve and register developer templates

## `POST /api/admin/verify-token`

Purpose:

- manually enqueue or trigger verification

## `POST /api/admin/project/hide`

Purpose:

- hide projects from public frontend views
