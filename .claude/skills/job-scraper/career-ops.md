# Career Ops employer-board supplement

Use the official [Career Ops scanner](https://github.com/career-ops-hq/career-ops/blob/main/modes/scan.md) for public employer boards. The tracked [portal configuration](career-ops-portals.yml) is the starting list. Keep the upstream checkout and dependencies under the repository's ignored `.career-ops-local/` directory. The scanner does not require a candidate profile for this use.

From the repository root, install once if the checkout is missing. Node 24 LTS and Git are sufficient for this scanner setup on Windows:

```powershell
git clone --depth 1 https://github.com/career-ops-hq/career-ops.git .career-ops-local
npm.cmd --prefix .career-ops-local install --ignore-scripts --omit=dev --no-audit --no-fund --cache .career-ops-local/.npm-cache
```

Run the scanner with the tracked configuration:

```powershell
$env:CAREER_OPS_PORTALS = (Resolve-Path '.claude/skills/job-scraper/career-ops-portals.yml').Path
node .career-ops-local/scan.mjs --dry-run --json
```

The preview receipt lists candidate URLs in `added_urls` and any source failures. Read the receipt even if the scan exits with an error: some boards can succeed while another fails. For a failed board, try its public employer list or a site-scoped web search. For example, use [Palantir's Seoul listings](https://jobs.lever.co/palantir?by=location&location=Seoul%2C+South+Korea) if its scanner request times out.

Make date and experience checks against the direct posting: some listings still accept applications without a reliable publication date. Keep the existing `ai-job-search` seen state as the only search history. Changes to watched companies belong in the tracked portal configuration. If a board is unsupported by the scanner, the main public web search can still look for that employer's postings.
