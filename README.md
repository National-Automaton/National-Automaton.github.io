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

The site publishes at <https://national-automaton.github.io/>. The first deploy can take a minute. The Pages settings screen shows the URL when it is live.

The repository is public, which GitHub Pages requires for an organization site on the free plan. A `.nojekyll` file is included so Pages serves these files as they are and does not run them through Jekyll.

## Custom domain

Add a `CNAME` file only when the domain is ready. Until then, leave it out so the `github.io` address keeps working.

1. Create a file named `CNAME` in the repository root. It should contain only the hostname, for example:

   ```
   www.example.com
   ```

   One line. No `https://`, no path, and no trailing slash.

2. Commit and push `CNAME`.

3. In **Settings → Pages**, enter the same hostname under **Custom domain** and save. GitHub reads it from the `CNAME` file.

4. At the DNS host, add the records in [GitHub’s custom-domain documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site):
   - For a `www` hostname, a `CNAME` record pointing at `national-automaton.github.io`.
   - For an apex domain (such as `example.com`), the `A` and `AAAA` records GitHub lists.

5. After DNS has propagated, turn on **Enforce HTTPS** in the Pages settings.

6. In `index.html`, update `canonical`, `og:url`, and `og:image` (and the matching Twitter image URL) so they use the custom domain. A comment in the file marks those tags.

## Contact address

`hello@nationalautomaton.com` is a placeholder. Search the source for `TODO` and replace it before relying on the link. It appears in the contact mailto, the footer mailto, and the JSON-LD `email` field.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The page |
| `styles.css` | Layout and type |
| `404.html` | Unknown paths on GitHub Pages |
| `favicon.svg` | Tab icon |
| `favicon.ico` | Fallback icon |
| `apple-touch-icon.png` | Home-screen icon |
| `og.png` | Social preview image (1200×630) |
| `fonts/` | OFL-licensed webfonts (Fraunces, Source Sans 3) |

## Font licenses

Fraunces and Source Sans 3 are subset static instances under the [SIL Open Font License](fonts/OFL.txt). The full license text is in `fonts/OFL.txt`.
