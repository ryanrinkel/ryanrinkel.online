# Tailored résumé template

Copy this whole folder to `r/<role>/` and edit its `index.html`.

## Checklist

- [ ] **Folder name is a role type, not a company.** These URLs get pasted into applications and
      sometimes forwarded. `r/devrel/`, not `r/anthropic/`.
- [ ] **Rewrite the summary paragraph** (`.r-summary`) for this role. It's the only part a busy
      reader is guaranteed to read.
- [ ] **Reorder or cut sections** so the most relevant experience is highest on page one.
- [ ] **Trim bullets.** A tailored résumé is shorter than the general one, not longer.
- [ ] **Update `<title>`** so the browser tab and any PDF export are named sensibly.
- [ ] **Print it** before sending. Ctrl/Cmd-P, destination "Save as PDF", and check where the
      page breaks land.

## What not to touch

- The `../../css/` links in `<head>` — they're what make this match the rest of the site.
- `<meta name="robots" content="noindex">` — keeps tailored versions out of search results.

The leading underscore hides this folder from the published site (Jekyll skips `_`-prefixed
directories), so the template itself never goes live.
