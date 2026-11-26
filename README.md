# NS-X.net — The Independent NSX Archive

A file-based digital library preserving the history, engineering and culture of the Honda / Acura NSX.

## Local development
Install Hugo (0.147.9 or newer), then run `hugo server`. Open http://localhost:1313. Build with `hugo --minify`; output is in public/.

## Cloudflare Pages
Connect this repository in Cloudflare Workers & Pages > Create > Pages > Connect to Git. Select main, Hugo, build command `hugo --minify`, output directory `public`, root directory blank, environment variable HUGO_VERSION=0.147.9. Deploy to the generated pages.dev address first. Add ns-x.net as a custom domain only after reviewing existing DNS/services; do not remove unrelated records. Each push to main triggers a deployment.

## Content
Edit Markdown in content/. Use section _index.md files and leaf page bundles (index.md). Keep large binaries and private masters out of Git. Publish approved media through a separate object store, eventually media.ns-x.net. Never assume possession implies redistribution rights.

The welcome experience, PDF pipeline, NSX Prime archive, and video preservation tooling are future migrations, not included in this bootstrap.
