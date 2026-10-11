# effect-workers-skill

An agent skill for writing Effect (`effect@4`) code that runs on Cloudflare
Workers: what may outlive a request, what may be cached per isolate, how to
build the router, keep startup CPU down, and where an MCP or RPC server
belongs.

Effect assumes a process that stays alive. A Worker only runs while a
request is open, and a timer or promise belongs to the request that made
it. The skill is the set of rules that kept a production Effect console on
Workers from hanging, written down after the fact.

## Install

Copy the skill into a project (or into `~/.claude/skills` for every project):

```sh
git clone https://github.com/mikepage/effect-workers-skill /tmp/effect-workers-skill
cp -R /tmp/effect-workers-skill/skills/effect-workers .claude/skills/
```

Use it together with Cloudflare's
[`workers-best-practices`](https://github.com/cloudflare/skills/tree/main/skills/workers-best-practices),
which covers Workers in general; this one covers only what is specific to
Effect.

## Background

- Repro: https://github.com/mikepage/effect-mcp-workers-repro
- Effect-TS/effect#9025: a long-lived fiber hangs once the request that
  scheduled its next turn has ended
- Effect-TS/effect#9026: a request-scoped `McpServer.layerHttp`

## License

MIT
