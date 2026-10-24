# National Automaton

Static landing page for National Automaton. Plain HTML and CSS, no build step, meant for GitHub Pages.

The name is **Automaton**, not Automation.

## Preview locally

From the repository root:

```bash
python3 -m http.server 8080
```

Open <http://localhost:8080>. Root-relative asset paths (`/styles.css`, `/fonts/…`) need a server; opening `index.html` as a file will not load them.

## Enable GitHub Pages

This repository is the organization site (`National-Automaton.github.io`). Pages serves it from the root of the default branch.

1. On GitHub, open **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Set the branch to **main** and the folder to **/ (root)**.
4. Save.

Until the custom domain below is serving traffic, the site is at <https://national-automaton.github.io/>. The first deploy can take a minute. The Pages settings screen shows the URL when it is live.

The repository is public, which GitHub Pages requires for an organization site on the free plan. A `.nojekyll` file is included so Pages serves these files as they are and does not run them through Jekyll.

## Custom domain

`CNAME` in the repository root contains exactly:

```
nationalautomaton.com
```

That is the hostname GitHub Pages will serve. It is an apex domain: no `www`, no `https://`, and no path. `index.html` already uses `https://nationalautomaton.com/` for the canonical URL, Open Graph URL, and social image.

The file takes effect on the branch Pages publishes (`main`). After it is on that branch:

1. On GitHub, open **Settings → Pages**.
2. Under **Custom domain**, confirm `nationalautomaton.com` and save. Publishing from a branch, GitHub keeps this in sync with `CNAME`.
3. Verify the domain for this organization so another repository cannot claim it. See [Verifying your custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages).
4. At the DNS host for `nationalautomaton.com`, add the apex records from [GitHub’s custom-domain documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site). Either all of these `A` and `AAAA` records, or one `ALIAS` / `ANAME` pointing at `national-automaton.github.io`:

   | Type | Name | Value |
   | --- | --- | --- |
   | `A` | `@` | `185.199.108.153` |
   | `A` | `@` | `185.199.109.153` |
   | `A` | `@` | `185.199.110.153` |
   | `A` | `@` | `185.199.111.153` |
   | `AAAA` | `@` | `2606:50c0:8000::153` |
   | `AAAA` | `@` | `2606:50c0:8001::153` |
   | `AAAA` | `@` | `2606:50c0:8002::153` |
   | `AAAA` | `@` | `2606:50c0:8003::153` |

   Remove any default apex record the DNS host adds (for example a parking `A` record) so it does not override these.

5. Optional: add a DNS `CNAME` record for `www.nationalautomaton.com` pointing at `national-automaton.github.io`. With the apex set as the Pages domain, GitHub redirects `www` to the apex. Do not change the repository `CNAME` file to `www`; that file names the primary host.

6. After DNS has propagated, turn on **Enforce HTTPS** in the Pages settings. That control can take up to a day to become available.

Check with:

```bash
dig nationalautomaton.com +noall +answer -t A
dig nationalautomaton.com +noall +answer -t AAAA
```

The answers should be the addresses above.

### nationalautomaton.ai

`nationalautomaton.ai` is a second domain. GitHub Pages serves one hostname from `CNAME`, which is `nationalautomaton.com`. Do not put the `.ai` name in that file.

Forward `nationalautomaton.ai` (and `www.nationalautomaton.ai`, if you use it) to `https://nationalautomaton.com` at the registrar or DNS host. A redirect there keeps a single site and a single canonical URL.

## Contact address

`hello@nationalautomaton.com` is a placeholder. Search the source for `TODO` and replace it before relying on the link. It appears in the contact mailto, the footer mailto, and the JSON-LD `email` field.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The page |
| `styles.css` | Layout and type |
| `404.html` | Unknown paths on GitHub Pages |
| `favicon.svg` | Crisp gold-on-black grid icon |
| `assets/favicon-32.png`, `favicon.ico` | Favicon cropped from the core-memory grid |
| `apple-touch-icon.png` | Home-screen icon from the same grid |
| `og.jpg` | Social preview: the logo on black (1200×630) |
| `assets/logo.jpg` | Optimized logo lockup |
| `assets/logo-web.jpg` | Smaller logo used in the hero |
| `assets/mark.png` | Core-memory grid, used in the header |
| `CNAME` | GitHub Pages hostname: `nationalautomaton.com` |
| `fonts/` | OFL-licensed webfonts (Fraunces, Source Sans 3) |

## Font licenses

Fraunces and Source Sans 3 are subset static instances under the [SIL Open Font License](fonts/OFL.txt). The full license text is in `fonts/OFL.txt`.
