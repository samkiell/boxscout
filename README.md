# boxscout

[![skills.sh installs](https://skills.sh/b/samkiell/boxscout)](https://skills.sh/samkiell/boxscout)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

**Give your coding agent a real browser. Find broken user flows before your users do.**

BoxScout is an open-source [Agent Skill](https://agentskills.io/) that walks through a live website on a cloud desktop, checks what actually happened, and reports failures with evidence. Powered by [box by Simular](https://box.simular.ai/) through MCP.

Describe a URL and a flow. BoxScout tests it step by step and returns an actionable pass/fail report.

## Quick start

**Prerequisites:** Node.js 22.20+ for the current Skills CLI, a coding agent that supports skills, and a [Simular Box](https://box.simular.ai/) account.

### 1. Install BoxScout

From your project directory:

```bash
npx skills add samkiell/boxscout --skill boxscout
```

For access in all projects, add `-g`:

```bash
npx skills add samkiell/boxscout --skill boxscout -g
```

Or target a specific coding agent:

```bash
# Claude Code
npx skills add samkiell/boxscout --skill boxscout -a claude-code -y

# Google Antigravity
npx skills add samkiell/boxscout --skill boxscout -a antigravity -y
```

The Skills CLI installs the skill's instructions. It does **not** connect or pay for the Simular Box cloud computer.

### 2. Connect your agent to Simular Box

```bash
npx @simular-ai/box connect
```

Alternatively, for Claude Code:

```bash
claude mcp add --transport http box https://mcp.box.simular.ai/mcp
```

Authenticate with Simular Box when prompted. Confirm your agent can access the `box` MCP tools before testing.

### 3. Test a website

Ask your agent:

> Use boxscout to smoke test https://your-staging-site.example. Check the homepage, navigation, and primary CTA. Report failures with evidence.

Or test a specific flow:

> Use boxscout to test signup and login on https://your-staging-site.example using my test credentials.

For a ticketing workflow, see [this example](examples/ticketing-checkout.md).

## What it does

- Runs browser walkthroughs for smoke tests, signup, login, and checkout
- Confirms the expected result after every step, instead of blindly chaining clicks
- Records PASS, FAIL, or BLOCKED for each step with visible evidence
- Sorts problems by severity and creates a developer-friendly report
- Stops before real payments and does not bypass CAPTCHA or 2FA

## How it works

BoxScout is **an agent skill, not a standalone browser automation server**. The skill teaches your existing coding agent how to use Simular Box's remote browser through MCP. Every user needs their own agent and Box connection.

```text
skills/boxscout/
  SKILL.md                    agent instructions
  references/flows.md         reusable test checklists
  references/report-template.md
examples/                     example prompts
```

## Limitations and safety

- Computer-use agents are slower and less reliable than deterministic scripted tests. A PASS means the flow worked in that run, not that it always works.
- Use staging environments and disposable test accounts. Never put secrets in prompts, screenshots, or reports.
- Simular Box requires a separate account and may consume usage credits. BoxScout does not include free unlimited browser compute.
- Don't run real payment transactions or destructive production actions without explicit approval.
- For critical regression checks, use BoxScout alongside Playwright or other scripted tests.

## Contributing

Bug reports, new flow checklists, and tested examples are welcome. Open an [issue](https://github.com/samkiell/boxscout/issues) with reproduction steps or submit a pull request. Please include the target environment, steps taken, expected result, and actual result. Redact credentials and customer data.

## Roadmap

- [ ] Test on 3 deployed applications and publish redacted reports
- [ ] Add an event ticketing checklist (QR codes, seat limits)
- [ ] Improve mobile viewport testing
- [ ] Build a GitHub Action wrapper that reports on pull requests
- [ ] Record a short public demo

## License

MIT, samkiel
