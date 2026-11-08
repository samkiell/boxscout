# Example prompt: ticketing checkout

Paste this into Claude Code (or any agent) with box and the boxscout skill installed:

> Use boxscout to test the checkout flow on https://your-staging-url.example. Pick any event, select 2 tickets, go to checkout, and stop before real payment. Report anything broken, sorted by severity.

Expected output: a report following `skill/boxscout/references/report-template.md`.
