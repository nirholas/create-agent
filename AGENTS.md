# AGENTS.md

Guidance for AI coding agents working in this repository.

## What this is

`@three-ws/create-agent` v0.1.0. One command from a sentence to a rigged, animated 3D agent you can embed anywhere. npm create @three-ws/agent "a friendly cartoon astronaut"

A JavaScript library. Import it from ESM.

## Use it

```bash
npx -y @three-ws/create-agent
```

Full usage, tool list and configuration are in [README.md](README.md). Machine-readable summaries: [llms.txt](llms.txt) and [llms-full.txt](llms-full.txt).

## Develop

```bash
npm install
node --check src/index.js
```


## Conventions

- ES modules, Node >=18.
- Read-only by default. Anything that signs, spends or sends must be an explicit, separately named tool or option, and must never be inferred from untrusted text (token names, memos, listings).
- Never commit credentials. Configuration comes from environment variables documented in the README.
- Keep changes small and covered by a test next to the code they change.

## Source of truth

This repository is a generated mirror of `packages` in https://github.com/nirholas/three.ws. Open issues here; send substantial changes as a pull request here or upstream.
