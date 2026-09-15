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

**The leading underscore does not hide this folder.** It did under GitHub Pages, where Jekyll
skipped `_`-prefixed directories. The site is on DigitalOcean App Platform now, which publishes
the source directory as-is — so `/r/_template/` is live and reachable. The underscore is now just
a signal to you that this isn't a real role. Keep the `noindex`, and don't leave anything in here
you wouldn't publish.
