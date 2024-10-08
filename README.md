<h1 align="center">Nimiq Validators</h1>

<p align="center">
  <a href="https://validators-api.pages.dev">
    <img src="./public/favicon.svg" alt="Nimiq Validators" width="64" />
  </a>

<p align="center">
Details of validators in the Nimiq Blockchain and their scores, calculated using Nimiq's VTS algorithm.
<p>

> [!NOTE]
> If you're a validator and would like to add your data to the API, please open a pull request (PR) with your JSON file, following the structure of `./public/validators/.example` in the `./public/validators` directory.

## Validators Dashboard

https://validators-api.pages.dev/

The dashboard is a simple Nuxt application that displays all validators and their scores.

## Validators API

| Endpoint                                                                       | Description                                                       |
| ------------------------------------------------------------------------------ | :---------------------------------------------------------------- |
| [/api/v1/scores](https://validators-api.pages.dev/api/v1/scores)               | An endpoint that returns the list of validators and their scores. |
| [/api/v1/scores/health](https://validators-api.pages.dev/api/v1/scores/health) | An endpoint that returns the state of the database.               |

## Validator Score

[Source code](./packages/nimiq-validators-score/)

This is a npm package that calculates the Trust Score of a validator. You can read more about the Score [here](https://validators-api.pages.dev/scores).

## Validator Details

The validator details are hardcoded into the [server/database/seed.ts](./server/database/seed.ts) file. If you are responsible for a validator and want to update the information, please open a PR with your information. This process may change in the future.

### Development

```bash
pnpm install
pnpm dev
```

> [!Note]
> We use [Nuxt Hub](https://hub.nuxt.dev) which uses Cloudflare Pages + Cloudflare D1 databases. The database is a sqlite instance and currently the database is remote for both development and production. You can change this behaviour in nuxt.config.ts.

We use Drizzle to access the database.

### Calculating the score using Nitro Tasks

To calculate the score, we need to run two processes: the fetcher and the score calculator. We do this using a Nitro Task, which is currently an experimental feature of Nitro. Nitro Task is a feature that allows you to trigger an action in the server programmatically or manually from the Nuxt Dev Center(go to tasks page).

Read more about the process of computing the score in the [nimiq-validators-score](./packages/nimiq-validators-score/README.md) package.

#### Database

As well as storing the [Validator Details](#validator-details), we also store the data produced by the fetcher in a sqlite database. This data is then used in the score calculator to compute the score. You can see the file [schema.ts](./server/database/schema.ts).

## Development

Once it is cloned and installed the dependencies, you must run:

```bash
pnpm db:generate
pnpm dev # or pnpm dev:remote to use the remote database
```
