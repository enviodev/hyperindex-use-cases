# HyperIndex use cases

Ready-to-run indexers built with [HyperIndex](https://docs.envio.dev/docs/HyperIndex/overview). Each one follows a real onchain activity, like a vault, a bridge or a DEX program, keeps the data up to date as new blocks arrive, and serves it over GraphQL.

Pick the one closest to what you're building, point it at your own contract or program, and deploy it. Each one ships with a prompt you can paste into Claude Code or Cursor if you'd rather your agent did the editing.

If you only need an answer, or a one-off backfill, the scripts in [hypersync-use-cases](https://github.com/enviodev/hypersync-use-cases) are quicker. Reach for an indexer when you need the data live behind an API.

## Indexers

### In this repo

| Indexer | Chain | How to |
| --- | --- | --- |
| [solana-dex-swaps-by-program](solana-dex-swaps-by-program) | Solana | Index every swap on Solana's main DEX programs, direct and routed |
| [solana-subscriptions](solana-subscriptions) | Solana | Index every plan, subscription and pull on Solana's Subscriptions program |
| [privacy-rings-solana](privacy-rings-solana) | Solana | Index every deposit, withdrawal and private transfer on a Solana privacy program |

### In their own repos

| Indexer | Chain | How to |
| --- | --- | --- |
| [solana-usdc-24h-indexer](https://github.com/enviodev/solana-usdc-24h-indexer) | Solana | Index every USDC transfer on Solana, inner transfers included |
| [metamask-money-account-indexer](https://github.com/enviodev/metamask-money-account-indexer) | Monad | Index every MetaMask Money Account deposit, withdrawal and balance |
| [elysium-hype-deposits-indexer](https://github.com/enviodev/elysium-hype-deposits-indexer) | HyperEVM | Index every HYPE deposit into Elysium through its bridge |
| [elysium-uniswap-v4-indexer](https://github.com/enviodev/elysium-uniswap-v4-indexer) | Elysium | Index every Uniswap v4 pool on Elysium over RPC |

## Quick start

You need Node 22.15 or newer, pnpm and Docker, plus a free API token from [envio.dev/app/api-tokens](https://envio.dev/app/api-tokens).

```bash
git clone https://github.com/enviodev/hyperindex-use-cases.git
cd hyperindex-use-cases/solana-dex-swaps-by-program
cp .env.example .env    # then paste your token into ENVIO_API_TOKEN
pnpm install
pnpm codegen
pnpm dev
```

Each indexer's README has its own finding, what it stores, the GraphQL queries to try, how to make it live and how to deploy it on [Envio Cloud](https://docs.envio.dev/docs/HyperIndex/hosted-service).

## Use these indexers with an AI agent

This repo ships with Envio's agent skills in `.claude/skills/`, so Claude Code, Cursor or any coding agent can work on it with the docs in context. Open an indexer's folder and paste something like this:

```text
This is an Envio HyperIndex indexer. Read README.md, config.yaml, schema.graphql,
the handlers in src/ and the skills in .claude/skills, then the docs at
https://docs.envio.dev/llms.txt.

Change it to index <YOUR CONTRACT OR PROGRAM> on <CHAIN>. Keep the tests working, add
one new entity and one handler for <EVENT OR INSTRUCTION>, run `pnpm codegen` and
`pnpm test` until they pass, then run `pnpm dev` and show me a GraphQL query for it.
```

Agents read docs best as plain text, so point yours at [docs.envio.dev/llms.txt](https://docs.envio.dev/llms.txt).

## FAQ

**What is HyperIndex?**
It's Envio's indexing framework. You choose the contracts and events to track, write TypeScript handlers that shape the data, and HyperIndex keeps it up to date across EVM chains and Solana and serves it as a GraphQL API. The [overview](https://docs.envio.dev/docs/HyperIndex/overview) has the details.

**How is it different from a HyperSync script?**
A script reads the data once and prints an answer. An indexer keeps running, stores what it reads and lets your app query it. HyperIndex uses [HyperSync](https://docs.envio.dev/docs/HyperSync/overview) under the hood to read the chain quickly.

**Does it work on Solana?**
Yes. See [HyperIndex on Solana](https://docs.envio.dev/docs/HyperIndex/solana).

**How do I deploy one?**
Push it to GitHub and deploy it on [Envio Cloud](https://docs.envio.dev/docs/HyperIndex/hosted-service) to get a hosted GraphQL endpoint.

## Links

- [HyperIndex overview](https://docs.envio.dev/docs/HyperIndex/overview)
- [HyperIndex on Solana](https://docs.envio.dev/docs/HyperIndex/solana)
- [Envio Cloud](https://docs.envio.dev/docs/HyperIndex/hosted-service)
- [HyperSync use cases](https://github.com/enviodev/hypersync-use-cases)
- [Get an API token](https://envio.dev/app/api-tokens)
- [Envio Discord](https://discord.gg/envio)

MIT licensed. Got an idea for an indexer, or stuck on one? Come say hi in the [Envio Discord](https://discord.gg/envio).
