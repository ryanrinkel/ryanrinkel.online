# ryanrinkel.online — portfolio &amp; résumé

Personal site for Ryan Rinkel. A code portfolio on the landing page, a résumé one click away,
and per-role tailored résumés for job applications.

Static HTML and CSS. No build step, no dependencies, no JavaScript beyond two lines
(a copyright year and a print button). Deployed with GitHub Pages.

## Layout

| Path | What it is |
|------|------------|
| `index.html` | Landing page — the portfolio. Hero, featured project, project grid, background, contact. |
| `resume.html` | The résumé. Dark on screen, black-on-white when printed. |
| `css/style.css` | Shared design tokens, nav, cards, footer. Used by every page. |
| `css/resume.css` | Résumé-specific layout **and the print stylesheet** (this is what makes the PDF). |
| `r/_template/` | Template to copy for a new tailored résumé. Hidden from the built site by Jekyll (leading `_`). |
| `r/<role>/` | One tailored résumé per role type, e.g. `r/devrel/`. |
| `CNAME` | Custom domain for GitHub Pages. |

## Two kinds of visitor

- **Someone browsing** (`/`) lands on the portfolio, sees the code, and can reach the résumé.
- **Someone you applied to** gets a direct `/r/<role>/` link that opens *their* tailored résumé
  immediately — no landing page in the way.

## Editing the content

Everything is in the HTML, in plain prose. There is no CMS and no templating layer, which means
editing is just finding the text and changing it.

- **Add a project** — copy an `<article class="card">` block in `index.html` and fill it in.
  Use `<span class="badge badge-wip">` for in-progress work or `badge-private` for closed source.
- **Change a résumé bullet** — edit `resume.html` directly. `ryan-rinkel-resume-devrel.md` in the
  repo root is the source-of-truth draft; keep the two in sync when you make a real change.
- **Retune the PDF** — everything that affects print lives in the `@media print` block at the
  bottom of `css/resume.css`. Font sizes there are in `pt` on purpose.

## Add a tailored résumé

1. Copy `r/_template` to `r/<role>` — a role **type**, never a company name, since these URLs
   get shared. `r/devrel`, `r/solutions-engineer`, `r/technical-writer`.
2. Edit that folder's `index.html`: trim bullets, reorder sections, sharpen the summary for the role.
3. Commit, push, and send `https://hireme.ryanrinkel.online/r/<role>/`.

The template is already wired to `../../css/`, so it picks up the shared styles and the print
stylesheet automatically. It carries `noindex` so tailored versions stay out of search results.

## Run it locally

No tooling required — open `index.html` in a browser. To check relative paths the way GitHub
Pages serves them:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## Deploying

GitHub Pages, served from the default branch. The custom domain lives in `CNAME`; point a DNS
`CNAME` record for that subdomain at `ryanrinkel.github.io`, then enable **Enforce HTTPS** in
the repo's Pages settings once the certificate is issued.

## History

This replaces [`hire-me-video`](https://github.com/ryanrinkel/hire-me-video), which led with an
AI-generated video resume. The work is still in that repo; this site leads with code instead.
