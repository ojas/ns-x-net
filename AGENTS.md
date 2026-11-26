# Agent guidance

Use Hugo, plain Markdown and portable metadata. Main site: Vercel at https://www.ns-x.net/; source repository: ojas/ns-x-net. Keep bulk binaries and private originals outside Git. Public media belongs in Cloudflare R2 (`ns-x-net-public`, custom hostname `media.ns-x.net`); do not put R2 credentials in repository files or logs.

Record provenance, attribution, publication rights and privacy review before publishing. Do not assume possession grants redistribution rights. Use `scripts/publish-media` for approved media: dry-run first; `--execute --approved` only after review. Do not use destructive `rclone sync`, modify bucket ACLs, create public access for private originals, or change DNS without owner approval.

Preserve existing content and stable URLs. Do not change hosting providers or migrate services without owner approval. Run `hugo --minify` before submitting site changes when available. Keep media paths portable and separate from Vercel.
