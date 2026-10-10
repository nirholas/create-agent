# @three-ws/create-agent

<!-- three.ws:badges -->
[![GitHub stars](https://img.shields.io/github/stars/nirholas/create-agent?style=flat&logo=github)](https://github.com/nirholas/create-agent/stargazers) [![License](https://img.shields.io/github/license/nirholas/create-agent?style=flat)](https://github.com/nirholas/create-agent/blob/HEAD/LICENSE) [![Last commit](https://img.shields.io/github/last-commit/nirholas/create-agent?style=flat)](https://github.com/nirholas/create-agent/commits) [![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat)](https://github.com/nirholas/create-agent/pulls) [![AI agent friendly](https://img.shields.io/badge/AI%20agents-AGENTS.md%20%2B%20llms.txt-6d5dfc?style=flat)](https://github.com/nirholas/create-agent/blob/HEAD/AGENTS.md)
<!-- /three.ws:badges -->


**One command from a sentence to a rigged 3D character you can put on your site.**

```bash
npm create @three-ws/agent "a friendly cartoon astronaut in a glossy white suit"
```

```
three.ws building "a friendly cartoon astronaut in a glossy white suit"
  a rigged humanoid, free lane, no account needed

· sent to the three.ws forge
· generating the figure (15s)
· generating the figure, then the skeleton (60s)
✓ model ready
· downloading the model

Friendly Cartoon Astronaut is ready in 94s

  folder  a-friendly-cartoon-astronaut/
          index.html
          agent.json
          README.md
          agent.glb (3.4 MB)
  viewer  https://three.ws/viewer?src=…

  Paste this anywhere:

  <script type="module" src="https://three.ws/agent-3d/latest/agent-3d.js"></script>

  <agent-3d body="https://three.ws/cdn/…/rigged.glb"
            name="Friendly Cartoon Astronaut"
            style="width:100%;max-width:420px;height:520px"></agent-3d>

  Open the demo:  npx serve a-friendly-cartoon-astronaut
```

No account. No API key. No signup. The generation runs on the three.ws free lane, and the platform's own provider keys cover it.

## What you get

| File | What it is |
| --- | --- |
| `agent.glb` | The model, with a humanoid skeleton, so it can be posed and animated. Opens in Blender, Unity, Godot, or any glTF tool. |
| `index.html` | A working demo page. Double click it. |
| `agent.json` | The record: prompt, hosted URLs, backend, timing. |
| `README.md` | How to embed it and where to go next. |

## Options

```bash
npm create @three-ws/agent "a knight in worn steel armor" --out ./knight
npm create @three-ws/agent --photo https://example.com/me.jpg --name "Me"
npm create @three-ws/agent "a small ceramic frog figurine" --object
```

| Option | Meaning |
| --- | --- |
| `--photo <url>` | Build from a public https reference image instead of a description |
| `--out <dir>` | Where to write the project (default: a slug of the description) |
| `--name <name>` | Display name (default: derived from the description) |
| `--object` | An object or prop (mesh only, free lane) instead of a rigged character |
| `--no-download` | Keep the hosted model URL, skip writing `agent.glb` |
| `--json` | Print the result as JSON and nothing else |
| `--origin <url>` | API origin (default `https://three.ws`) |

Describe **one full-body humanoid in a neutral standing pose** for the best rig. Lead with the subject, then materials and colours: the free lane conditions on roughly the first 77 characters, so front-load what matters.

## Programmatic use

```js
import { createAgent } from '@three-ws/create-agent';

const made = await createAgent({
	prompt: 'a friendly cartoon astronaut',
	out: './astro',
	onProgress: ({ message }) => console.log(message),
});

made.result.glbUrl; // hosted, durable
made.result.rigged; // true
made.dir; // absolute path to the project
```

| Export | What it does |
| --- | --- |
| `createAgent(opts)` | The whole pipeline: generate, scaffold, download |
| `callForge({ tool, args, ... })` | One forge call (`forge_avatar` or `forge_free`) |
| `downloadModel(url)` | Fetch the model bytes with a deadline |
| `projectFiles(...)`, `demoPage(...)`, `embedSnippet(...)` | The scaffold, as pure functions |
| `ForgeError` | Carries `code`: `timeout`, `unreachable`, `no_model`, `rpc_error`, `http_<status>` |

Everything takes `{ fetchImpl, signal, origin }`, so it runs against a local three.ws, a proxy, or a test double.

## How long it takes

A rigged character is generation plus rigging, usually one to three minutes; rigging is the slow half. An `--object` is faster. Every call carries an explicit deadline (10 minutes) and reports real elapsed time, never an invented progress bar. If the deadline hits, the job may still finish: finished models land at <https://three.ws/creations>.

## Related

- The full pipeline in a browser: <https://three.ws/create>
- `<agent-3d>` attribute reference: <https://three.ws/docs/web-component>
- Your agent's live status on a home screen or in a README: [@three-ws/agent-glance](../agent-glance)
- Docs: <https://three.ws/docs/create-agent>

## License

Apache-2.0

<!-- three.ws:growth -->
## Support the project

If create-agent saves you time, **[star it on GitHub](https://github.com/nirholas/create-agent)**. Stars are how other developers and AI agents find the repositories worth trusting, and they cost you one click.

Know someone who would use it? [Post on X](https://twitter.com/intent/tweet?text=create-agent%3A%20One%20command%20from%20a%20sentence%20to%20a%20rigged%2C%20animated%203D%20agent%20you%20can%20embed%20anywhere&url=https%3A%2F%2Fgithub.com%2Fnirholas%2Fcreate-agent) · [Share on Bluesky](https://bsky.app/intent/compose?text=create-agent%3A%20One%20command%20from%20a%20sentence%20to%20a%20rigged%2C%20animated%203D%20agent%20you%20can%20embed%20anywhere%20https%3A%2F%2Fgithub.com%2Fnirholas%2Fcreate-agent) · [Share on LinkedIn](https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Fgithub.com%2Fnirholas%2Fcreate-agent) · [Submit to Hacker News](https://news.ycombinator.com/submitlink?u=https%3A%2F%2Fgithub.com%2Fnirholas%2Fcreate-agent&t=create-agent%3A%20One%20command%20from%20a%20sentence%20to%20a%20rigged%2C%20animated%203D%20agent%20you%20can%20embed%20anywhere) · [Share on Reddit](https://www.reddit.com/submit?url=https%3A%2F%2Fgithub.com%2Fnirholas%2Fcreate-agent&title=create-agent%3A%20One%20command%20from%20a%20sentence%20to%20a%20rigged%2C%20animated%203D%20agent%20you%20can%20embed%20anywhere)

## Built for AI agents too

Coding agents and LLM tooling can read this repo directly: [AGENTS.md](./AGENTS.md), [llms.txt](./llms.txt), [llms-full.txt](./llms-full.txt). Point an agent at `https://github.com/nirholas/create-agent` and it has the context it needs.

## More from the same author

- [All repositories by nirholas](https://github.com/nirholas/nirholas#readme): the full catalog, grouped by topic
- [three.ws](https://three.ws): the platform for 3D AI agents with Solana wallets, a skill marketplace and x402 payments
- Questions or ideas: [open an issue](https://github.com/nirholas/create-agent/issues) or [start a discussion](https://github.com/nirholas/create-agent/discussions)

## Contributors

[![Contributors](https://contrib.rocks/image?repo=nirholas/create-agent)](https://github.com/nirholas/create-agent/graphs/contributors)

## Star history

[![Star History Chart](https://api.star-history.com/svg?repos=nirholas/create-agent&type=Date)](https://www.star-history.com/#nirholas/create-agent&Date)

<!-- /three.ws:growth -->

<!-- three.ws:ecosystem -->
## Part of three.ws

[three.ws](https://three.ws) is a platform for 3D AI agents with Solana wallets: avatars, a skill marketplace, x402 payments and more than seventy MCP servers. `@three-ws/create-agent` is one package from it.

- Documentation site: https://nirholas.github.io/create-agent/
- npm: https://www.npmjs.com/package/@three-ws/create-agent
- Canonical source: https://github.com/nirholas/three.ws (this repository is a generated mirror of `packages/create-agent`)
- Agent-readable summary: [llms.txt](./llms.txt) and [AGENTS.md](./AGENTS.md)
- Issues and ideas: https://github.com/nirholas/create-agent/issues
<!-- /three.ws:ecosystem -->
