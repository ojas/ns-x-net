# NS-X.net — The Independent NSX Archive

A file-based digital library preserving the history, engineering and culture of the Honda / Acura NSX.

## Hosting and local development

The primary Hugo site is deployed from `main` to **Vercel** at https://www.ns-x.net/ (project: https://vercel.com/ojas-patels-projects/ns-x-net). `vercel.json` pins Hugo and builds to `public/`. The existing `wrangler.toml` is not used by Vercel.

Install Hugo 0.147.9 or newer, then run `hugo server` (http://localhost:1313). Build with `hugo --minify`.

## Content and media

Edit Markdown in `content/`. Use section `_index.md` files and leaf page bundles (`index.md`). Git stores site source, metadata and manifests, **not** bulk media or private masters.

Public media lives in Cloudflare **R2**, independently of Vercel:
- rclone remote: `nsx-r2` (local convention; configure it yourself)
- public bucket: `ns-x-net-public` (expected name; override via environment)
- public URL base: `https://media.ns-x.net` (only works after the R2 custom domain is configured)

R2 is S3-compatible. Configure `rclone config` with storage `s3`, provider `Cloudflare`, endpoint `https://<ACCOUNT_ID>.r2.cloudflarestorage.com`, region `auto`, and a bucket-scoped R2 API key. Leave S3 `acl` and `bucket_acl` empty. Do not commit credentials. Public object access is controlled by the R2 custom domain, **not** S3 ACLs or CORS. CORS only governs cross-origin browser access.

### Publishing approved media

Requires Python 3 and rclone on PATH. The tool is **dry-run by default**, never deletes remote objects, and requires explicit confirmation for writes.

```sh
# Inspect planned upload (no changes)
python3 scripts/publish-media ~/NSX-Publish/brochure.pdf documents/brochures/brochure.pdf

# Upload after verifying rights, attribution and privacy
python3 scripts/publish-media ~/NSX-Publish/brochure.pdf documents/brochures/brochure.pdf --execute --approved

# Upload a directory, preserving relative paths
python3 scripts/publish-media ~/NSX-Publish/scans images/scans --execute --approved
```

Use `NSX_R2_REMOTE`, `NSX_R2_BUCKET`, and `NSX_MEDIA_BASE` to override defaults. The script prints the corresponding public URLs. It verifies directory uploads by remote file sizes; single-file uploads are checked for remote existence, not cryptographic equivalence. For irreplaceable data, retain local checksums and independently backed-up originals. Uploading to R2 is **publication**, not a substitute for backup.

Workflow: immutable local master → local publication staging → rights/privacy review → dry run → upload and verify → Hugo metadata → Git commit → Vercel deployment. Avoid `rclone sync` against the public bucket: it may delete objects.

The welcome experience, PDF pipeline, NSX Prime archive, and video preservation tooling are future migrations, not included in this bootstrap.
