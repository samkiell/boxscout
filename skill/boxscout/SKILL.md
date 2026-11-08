---
name: boxscout
description: QA a deployed website or web app by driving a real browser on a cloud desktop through the box MCP server (box by Simular). Use this skill whenever the user wants to test, smoke test, click through, sanity check, or find bugs in a live URL, a staging site, a signup, login or checkout flow, or a hackathon demo before submission, even if they do not say "QA". Produces a pass/fail report with evidence for each step. Requires the box MCP server to be connected.
---

# boxscout

Walk through a live web app like a real user, record what happens, and report what broke.

## Requirements

- The `box` MCP server must be connected. If its tools are not available, stop and tell the user to run `npx @simular-ai/box connect` or add `https://mcp.box.simular.ai/mcp` as a remote MCP server, then retry.
- A target URL. If the user gave none, ask for it. One question only.

## Inputs to collect

Ask only for what is missing, and prefer sensible defaults over questions.

1. Target URL (required).
2. Flow to test. Default: homepage load, main navigation, and the primary call to action.
3. Test credentials, if the flow needs login. Never invent real accounts. Never use real payment details.
4. Viewport. Default: desktop. Offer mobile width as a second pass.

## Workflow

1. **Plan.** Write a numbered list of steps for the flow before touching the browser. Keep it under 15 steps. For common flows, read `references/flows.md` and adapt the matching checklist.
2. **Open the target** in the box browser. Wait for the page to settle, then take a screenshot.
3. **Execute step by step.** After every action, read the screen and confirm the expected result happened. Do not chain several actions blind.
4. **Record evidence.** For each step, note: action taken, expected result, actual result, status (PASS, FAIL, BLOCKED), and a screenshot reference for any FAIL.
5. **On failure,** retry once to rule out a slow load. If it still fails, mark FAIL, describe exactly what you saw, and continue with later steps that do not depend on it. Mark dependent steps BLOCKED.
6. **Check the basics on every page visited:** visible error messages, broken images, layout overflow, console errors if the box exposes them, and links that lead nowhere.
7. **Report.** Use `references/report-template.md`. Lead with a one line verdict, then failures sorted by severity, then the full step log.

## Safety rules

- Never submit real payments, send real emails, or create data in a production system unless the user explicitly confirms. Use test mode, test cards documented by the provider, or stop before the final submit.
- Never store, echo, or log credentials in the report. Redact them.
- Stay on the target domain unless the flow requires an external provider such as a payment page. Say when you leave it.
- If you hit a CAPTCHA, a 2FA prompt, or anything that needs a human, mark the step BLOCKED and say why. Do not try to bypass it.
- Do not run load tests or repeated rapid requests. This is a functional walkthrough, not a stress test.

## Severity guide

- **Critical:** the main flow cannot be completed (cannot sign up, cannot pay, page does not load).
- **Major:** the flow completes but with wrong data, broken states, or a clear usability failure.
- **Minor:** cosmetic issues, typos, slow but working steps.

## Honest limits

State these in the report when relevant. Computer use is slower and less reliable than scripted tests. A PASS here means "worked once for this agent," not "guaranteed to work for everyone." Recommend a scripted test for anything that must never regress.
