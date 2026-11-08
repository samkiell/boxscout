# boxscout

An agent skill that QAs a live website by driving a real browser on a cloud desktop. Built on [box by Simular](https://box.simular.ai/), which gives your coding agent a computer over MCP.

Point it at a URL, tell it the flow, get back a pass/fail report with evidence.

## What it does

- Walks through signup, login, checkout, or a plain smoke test like a real user
- Confirms each step worked before moving to the next
- Reports failures sorted by severity, with what it saw
- Stops before real payments and never bypasses CAPTCHAs or 2FA

## Setup

1. Connect box to your agent:
   ```bash
   npx @simular-ai/box connect
   ```
   Or for Claude Code:
   ```bash
   claude mcp add --transport http box https://mcp.box.simular.ai/mcp
   ```
   Then run `/mcp` and authenticate.

2. Install the skill. For Claude Code, copy the skill folder:
   ```bash
   cp -r skill/boxscout ~/.claude/skills/boxscout
   ```

3. Ask:
   > Use boxscout to test https://your-site.example. Flow: signup then login.

## Repo layout

```
skill/boxscout/
  SKILL.md                    the skill itself
  references/flows.md         checklists for common flows
  references/report-template.md
examples/                     sample prompts
```

## Limits

- Computer use agents are slower and less reliable than scripted tests. Treat a PASS as "worked once," not a guarantee.
- box is one desktop per account and its model calls use that account's daily credits. Every user brings their own box account.
- Use it on staging or test mode. Do not point it at production payments.

## Roadmap

- [ ] Test the skill on 3 real deployed apps and publish the reports
- [ ] Add a flow checklist for event ticketing (QR codes, seat limits)
- [ ] Mobile viewport second pass
- [ ] GitHub Action wrapper that posts the report on a pull request
- [ ] Demo video

## License

MIT, Samuel Ezekiel
