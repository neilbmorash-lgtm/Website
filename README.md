# neilmorash.ca

Personal site for Neil Morash. One static page: HTML, CSS, and a small script. There is no build step. Open `index.html` in a browser, or from this folder run:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080`.

Photos, the social share image, and the favicon are placeholders. The list of what to swap in is in [assets/README.md](assets/README.md).

## GitHub Pages

1. Merge this site to the `main` branch.
2. On GitHub, open the repository **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Set the branch to **main** and the folder to **/ (root)**. Save.

GitHub will publish the project site at `https://neilbmorash-lgtm.github.io/Website/` until the custom domain is serving. The address shown in Settings → Pages is the one to check first.

The `CNAME` file in the repo root contains:

```text
neilmorash.ca
```

That file is what attaches the apex domain. If you type the domain into the Pages **Custom domain** box and save, GitHub writes the same file. Keep it as a single line, with no `https://`.

After DNS is in place, turn on **Enforce HTTPS**. That checkbox can take up to 24 hours to appear.

`.nojekyll` is included so Pages serves the files as they are and does not run Jekyll.

## DNS

Add these records at the DNS host for `neilmorash.ca`. Remove any old A, AAAA, or CNAME records on the same names first, including a default parking-page record. Do not use a wildcard such as `*.neilmorash.ca`.

Changes can take up to 24 hours to propagate. Add the custom domain in the repository **before** you point DNS at GitHub, so the domain cannot be claimed by another project while it is unattached.

### Apex (`neilmorash.ca`)

Four **A** records. The name is `@` at most registrars (the apex itself).

| Type | Name | Value |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |

Optional **AAAA** records, for IPv6. GitHub recommends keeping the A records as well.

| Type | Name | Value |
| --- | --- | --- |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |

### www

Point `www` at the GitHub Pages user host, not at the repository name and not at `*.pages.github.io`.

| Type | Name | Value |
| --- | --- | --- |
| CNAME | `www` | `neilbmorash-lgtm.github.io` |

With `neilmorash.ca` saved as the custom domain, GitHub redirects `www.neilmorash.ca` to `https://neilmorash.ca`.

Check the records with:

```bash
dig neilmorash.ca +noall +answer -t A
dig neilmorash.ca +noall +answer -t AAAA
dig www.neilmorash.ca +nostats +nocomments +nocmd
```

The A answers should be the four addresses above. The www answer should be a CNAME to `neilbmorash-lgtm.github.io`.

## Featured video

The player on the page is [Take what you Love (Looping Improv)](https://www.youtube.com/watch?v=kXeGb1Epx74) from the [Neil Morash YouTube channel](https://www.youtube.com/@neilmorash) (channel ID `UCmWuSxh4aU1u3o4WZTso5tQ`). The newer upload from 10 November 2026 does not allow embedding. To feature a different upload, replace the video id in the iframe `src` in `index.html`.
