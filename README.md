# TinkerPro campaigns

`cloud-pos.json` controls the TinkerPro Cloud POS promotion inside installed
TinkerPro POS terminals (v1.6.0 and later). Terminals download it over HTTPS,
cache it for 6 hours, and keep working normally if it can't be reached.

Edits reach terminals within about 6 hours, with no POS release needed.

## Common changes

| To... | Change |
|---|---|
| Switch the promotion **off** everywhere | `"enabled": false` |
| Show it to only some terminals | `"rollout_percent": 10` (0–100) |
| Limit it to certain roles | `"roles": ["admin", "cashier"]` (empty = everyone) |
| Run it between dates | `"starts_at"` / `"ends_at"`, e.g. `"2026-12-31T23:59:59+08:00"` |
| Change the wording | `headline`, `description`, `benefits`, `cta_label`, `trial_label`, `peek_label` |
| Change the rotating pop-up lines | `messages_pos` (cashier), `messages_mgmt` (back office) |
| Change the links | `cta_url`, `trial_url` |

## Rules the terminals enforce

- `schema` must be `1` and `enabled` must be `true` (a real boolean) or nothing shows.
- `id`: lowercase letters, numbers and dashes. Keep it the same when you edit
  wording: "Remind me later" / "Don't show again" are remembered per `id`, so a
  new `id` shows the promotion again to everyone who dismissed it.
- Links must be `https://` on `tinkerpro.com`, `www.tinkerpro.com` or
  `cloud.tinkerpro.io`. Any other link makes the whole file invalid (hidden).
- Text is plain text only; HTML is stripped. Limits: headline 80, description
  280, button labels 40, each pop-up line 80 characters; up to 5 benefits and
  60 pop-up lines per list.
- Terminals older than `min_version` ignore the file.
- If the file is invalid or unreachable for 7 days, the promotion hides.
