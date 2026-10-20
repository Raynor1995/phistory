# Manually supplied traces

Model-exported JSON objects can use the same request-body structure. The importer accepts
one JSON object, either pretty-printed JSON or a single JSONL record. For model self-reports,
pass `--self-report --surface model-self-report --agent-id <id> --agent-name <name>`.
This records the source kind and labels both the rendered prompt and web detail as
model-reported content, not network evidence. The supplied timestamp determines the
archive time; the positional version remains the chosen version label.

Private runtime context blocks, agent names, teammate rosters and UUIDs are normalized
by shared rules. Review every new source before importing; the rules are not a guarantee
that arbitrary JSON contains no private data.

Keep the original JSONL outside this repository. Import a selected, single-request Claude Tag trace with:

```bash
uv run python scripts/import_manual_trace.py /path/to/selected-request.jsonl YYYY-MM-DD
uv run phistory render-index
uv run phistory translate --agents claude-tag --all-captured --prune
uv run phistory build-site --output .phistory-cache/site
uv run python scripts/audit_translations.py --site-dir .phistory-cache/site --require-complete
```

The importer applies the same policy to every version. It retains system instructions, interleaved system reminders, tool definitions, and cache boundaries; replaces private memory payloads, session links, emails, runtime paths, and transport identifiers with stable placeholders; removes the captured user text and later conversation content. Later non-system messages become one history placeholder, with their count recorded in `meta.json`. The original file's SHA-256 is recorded there too. `trace.jsonl` in the archive is redacted evidence, not a byte-for-byte copy of the source.

Review the resulting `prompt.md` and its diff before publishing. New source shapes or private data types may need a shared importer rule and a regression test. Do not add a version-specific replacement for a value that occurs across versions.
