# ryanrinkel.online — portfolio &amp; résumé

Personal site for Ryan Rinkel. A code portfolio on the landing page, a résumé one click away,
and per-role tailored résumés for job applications.

Static HTML and CSS. No build step, no dependencies, no JavaScript beyond two lines
(a copyright year and a print button). Deployed on DigitalOcean App Platform.

## Layout

| Path | What it is |
|------|------------|
| `index.html` | Landing page — the portfolio. Hero, featured project, project grid, background, contact. |
| `resume.html` | The résumé. Dark on screen, black-on-white when printed. |
| `css/style.css` | Shared design tokens, nav, cards, footer. Used by every page. |
| `css/resume.css` | Résumé-specific layout **and the print stylesheet** (this is what makes the PDF). |
| `r/_template/` | Template to copy for a new tailored résumé. Published like everything else — see the note below. |
| `r/<role>/` | One tailored résumé per role type, e.g. `r/devrel/`. |
| `404.html` | Not-found page. Wired up as the app's `error_document`. |

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

**On the leading underscore.** It's a leftover from GitHub Pages, where Jekyll skipped
`_`-prefixed directories and the template never shipped. App Platform has no Jekyll: it publishes
the source directory as-is, so `/r/_template/` *is* reachable on the live site. It carries
`noindex`, and it holds nothing but an empty résumé shell, so this is untidy rather than a leak —
but don't put anything in there you wouldn't publish.

## Run it locally

No tooling required — open `index.html` in a browser. To check root-relative paths (`/css/…`,
which `404.html` uses) the way the app serves them:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## Deploying

DigitalOcean App Platform, as a **static site** component pointed at this repo's `main` branch
with deploy-on-push enabled. Pushing to `main` is the deploy. There is deliberately no
`.do/app.yaml` in this repo — App Platform reads that file when a repo is connected, and a stale
copy of it will quietly hand a newly created app the wrong name, domain, or output directory.
The app is configured in the DO console, and the console is the single source of truth.

`ryanrinkel.online` is **registered at Bluehost but delegated to DigitalOcean's nameservers**
(`ns1/ns2/ns3.digitalocean.com`). DNS records are therefore edited in the DigitalOcean control
panel, not Bluehost's. Editing DNS at Bluehost has no effect unless the nameservers are moved
back there first.

`hireme.ryanrinkel.online` is a DNS `CNAME` to the app's `*.ondigitalocean.app` hostname, and
DigitalOcean terminates TLS. Because the domain is attached to the app rather than to a host
inferred from a file, there is **no `CNAME` file in this repo** — that file is a GitHub Pages
convention and does nothing here.

To watch a deploy: DO console → Apps → the app → **Activity**. To roll back, redeploy an earlier
commit from that same tab.

## History

This replaces [`hire-me-video`](https://github.com/ryanrinkel/hire-me-video), which led with an
AI-generated video resume. The work is still in that repo; this site leads with code instead.
