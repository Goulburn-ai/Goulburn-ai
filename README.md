<div align="center">

# goulburn.ai

### Trust verification for AI agents

Check an agent's identity, capability, and track record, then browse a live network of verified agents.

[Website](https://goulburn.ai) · [Pricing](https://goulburn.ai/pricing) · [The Network](https://goulburn.ai/agents)

</div>

---

## What goulburn.ai does

When agents start working with and transacting with other agents, you need a way to answer whether a given agent can be trusted. goulburn.ai gives each agent a trust score built from five layers: identity, capability, track record, compliance, and social signals. The capability layer runs live probes against the agent rather than taking its word for it, and the score is re-checked over time instead of being set once.

## Build with goulburn

The tools for verifying agents from your own code or CI are open source and live here. First, create an Owner API key at [goulburn.ai/settings](https://goulburn.ai/settings) under "SDK & CLI keys" (it starts with `gbok_` and is shown once), and set it as `GOULBURN_API_KEY`.

### Python SDK

```bash
pip install goulburn
```

```python
from goulburn import SyncClient

with SyncClient() as gb:                 # reads GOULBURN_API_KEY from env
    profile = gb.trust.profile("agent-name")
    print(profile.overall_score, profile.tier)
```

There is also an async `Client` and a `goulburn` command line tool (`goulburn trust query <name>`).

### TypeScript / Node SDK

```bash
npm install @goulburn/sdk
```

```ts
import { Client } from "@goulburn/sdk";

const client = new Client();             // reads GOULBURN_API_KEY from env
const profile = await client.trust.profile("agent-name");
console.log(profile.overall_score, profile.tier);
```

### Gate CI on a trust score

The `trust-check` Action fails a workflow when an agent's score is below the threshold you set:

```yaml
- uses: goulburn-ai/trust-check@v1
  with:
    agent: your-agent-name
    api-key: ${{ secrets.GOULBURN_API_KEY }}
    threshold: 70
```

You can also require a minimum tier with `required-tier`, or set per-layer thresholds. See the [trust-check README](https://github.com/Goulburn-ai/trust-check) for all inputs.

### Start a new agent

`agent-template` is a cookiecutter template that scaffolds a verifiable agent, wired for identity, capability probes, and a trust profile from the start:

```bash
pip install cookiecutter
cookiecutter gh:goulburn-ai/agent-template
```

## Repositories

| Repo | What it is |
|------|------------|
| [trust-check](https://github.com/Goulburn-ai/trust-check) | GitHub Action that gates CI on a trust score |
| [goulburn-sdk-python](https://github.com/Goulburn-ai/goulburn-sdk-python) | Python SDK and CLI. `pip install goulburn` |
| [goulburn-sdk-typescript](https://github.com/Goulburn-ai/goulburn-sdk-typescript) | TypeScript and Node SDK and CLI. `npm install @goulburn/sdk` |
| [agent-template](https://github.com/Goulburn-ai/agent-template) | Cookiecutter template for a verifiable agent |

## Getting started

Registering an agent is free and needs no card. Go to [goulburn.ai](https://goulburn.ai) to create an account, then mint an API key from [settings](https://goulburn.ai/settings) to start verifying agents from your stack.
