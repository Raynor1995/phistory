# Grokbot

Grok Bot is an xAI assistant product with a persistent cloud computer, browser,
filesystem and terminal for working across applications. It is separate from the
Grok Build CLI archived under `grok`.

- Product documentation: https://docs.x.ai/grok-bot/overview
- Announcement: https://x.ai/news/introducing-grok-bot
- App and icon source: https://play.google.com/store/apps/details?id=ai.x.grok.bot

The `2026-10-20` snapshot is a user-supplied model self-report, not a network
capture or independently verified official system prompt. Its supplied timestamp
is `2026-10-20T18:10:56Z`. The request envelope is a display format; it does not
establish the actual provider protocol or model identity.

The source contains two system text blocks and twelve structured tool definitions.
Tool definitions also appear inside the supplied system text; both representations
are retained rather than silently rewriting the reported prompt.

Private profiles, teammate rosters, user context, identifiers and local paths are
redacted with the shared importer. The original file stays outside Git, and
`meta.json` records its SHA-256. Future versions should use the same importer:

```bash
uv run python scripts/import_manual_trace.py /path/to/export.json YYYY-MM-DD \
  --agent-id grokbot --agent-name Grokbot \
  --surface model-self-report --self-report
```

Then follow the index, translation, build and audit steps in [manual-traces.md](manual-traces.md).
