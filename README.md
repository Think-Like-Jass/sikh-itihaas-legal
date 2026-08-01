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
- Each `content_manifest` entry carries an `updated_at` (ISO date). The app
  always fetches the small `master.json` when online and re-downloads ONLY the
  files whose `updated_at` changed since it last synced. **Bump `updated_at`
  (and the top-level one) whenever you edit a content file.** (`version` ints
  are kept too, but `updated_at` is what drives the resync.)
- Node order is driven by `sort_order`, not `year` (`year` is a display label).

See the app's `ai-assist/` docs for the full schema and conventions.
