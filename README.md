# National Automaton

Static personal portfolio for Michael Davis. Plain HTML and CSS, no build step, meant for GitHub Pages.

The page presents Code Automaton as one engineer's open-source work, not as a company
selling services. Keep it that way: no pricing, no "coming soon" product promises, no
enterprise-sales framing, and no integrations the repo does not actually ship. See
"Positioning" below.

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

## Product sections

`index.html` sections, in page order and anchored in the nav: `#code-automaton`, `#demo`, `#features`, `#why`, `#roadmap`, `#about`, `#contact`. `404.html` repeats the nav, so add or rename an anchor in both files.

The Code Automaton section states facts that live outside this repository (npm package name `code-automaton`, command `coda`, version, MIT license). When a release bumps the version, update the `Version` row in the `.spec` list and `softwareVersion` in the JSON-LD together.

## Demo video

`#demo` embeds a YouTube screencast of Code Automaton. It is a click-to-load facade: the page ships only the thumbnail from `i.ytimg.com`, and the `<iframe>` is injected from `www.youtube-nocookie.com` when the visitor presses play. Keep it that way — do not replace it with an autoloading iframe, which would add a third-party request to every page view.

The video ID is written out twice — `data-video` on `.video-facade` and the `video-poster` `src` — and the inline script builds the embed URL from `data-video`. To change the demo, update both and keep `data-video` authoritative for the player. The thumbnail uses `maxresdefault.jpg`, which only exists for videos uploaded at 1280×720 or larger; if a replacement video lacks it, fall back to `hqdefault.jpg` and drop the `width`/`height` attributes.

The video is a recording of a specific release (its YouTube title names the version), so it can lag the `Version` row. Leave the copy describing features rather than claiming it shows the current release.

### Playback quality

The embedded player chooses its starting resolution adaptively, from the player's rendered size and the viewer's bandwidth, and YouTube does not expose a supported way to lock it. The page does two things to push it toward 1080p:

- `#demo` uses `.wrap.video-wide` (up to 1280px) instead of the default 1080px wrap, so the player renders larger. Player size is the biggest real factor; keep this wide rather than reusing the plain `.wrap`.
- The embed URL appends `vq=hd1080`. This is a hint only — YouTube deprecated and may ignore it, especially alongside `autoplay=1`.

Neither is a guarantee: a viewer on a slow connection or in a small window will still get a lower resolution. If an exact fixed 1080p ever becomes a requirement, the only reliable route is self-hosting the file in a `<video>` element rather than embedding YouTube.

The screencast is terminal text, which is hard to read at low resolution, so `.video-note` tells the viewer that the quality control sits in the player's **top-right corner** (it is not in the usual bottom bar on the embedded player's current layout) and links to the full player on YouTube. Keep both: the note is the only signpost to the quality menu. The video is uploaded at 1080p — YouTube offers 144p through 1080p for it — so the source is not the limitation.

## Positioning

The page is written in the first person and names Michael. It deliberately omits:

- pricing, "open core", or paid tiers;
- Spend Automaton as a product — it appears only under "Roadmap and ideas", labeled as not built;
- ticketing/chat/email integrations, which do not exist in the repo.

Do not add claims that cannot be verified from the code: no usage or adoption numbers, no
"built with <tool>" statements, no integration or partnership claims. `#why` and `#about`
carry claims only Michael can confirm; check with him before editing them. `npm view code-automaton version` is the authority; the top-level registry document can lag, so prefer the per-version endpoint.

## Contact address

The site uses `info@nationalautomaton.com`. It appears in three places in `index.html`: the JSON-LD `email` field, the contact mailto, and the footer mailto. Update all three together if the address changes.

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
