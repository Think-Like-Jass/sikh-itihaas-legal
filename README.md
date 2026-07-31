# sikh-history-content

Remote content for the **ਸਿੱਖ ਇਤਿਹਾਸ** (Sikh History) Android app.

The app never bundles this content — it fetches these JSON files from GitHub raw
URLs, caches them in Room, and works offline after the first sync.

## Structure

```
master.json                       ← entry point (fetched first, always)
content/
  eras.json                       ← journey skeleton: all eras
  nodes/
    era_pichhokar.json            ← nodes for the ਪਿਛੋਕੜ era
    ...                           ← one file per era
  collections.json                ← (planned) cross-cutting curated lists
assets/
  icons/                          ← launcher/logo variants
  images/                         ← content images
```

## Rules

- All JSON keys are `snake_case`.
- Every user-visible string is a `{ "pa": "…" }` object (Punjabi mandatory;
  other languages optional). App resolves selected language → default `pa`.
- `version` integers in `master.json`'s `content_manifest` are bumped manually
  whenever a file changes — the app fetches only what changed.
- Node order is driven by `sort_order`, not `year` (`year` is a display label).

See the app's `ai-assist/` docs for the full schema and conventions.
