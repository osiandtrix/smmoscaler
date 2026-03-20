# Alpha's SimpleMMO Scaler (A.S.S.)

Made with love by Raven (Alpha, 28790).

A dedicated tool for SimpleMMO, an old-school browser MMORPG.

- Game: https://web.simple-mmo.com
- Tool: https://totallynotaduck.github.io/smmoscaler/

This project helps you find the best item choices based on your level and available gold. It uses a large item database logsheet and includes a built-in API caller/logging tool.

API calling runs at 1 request every 2 seconds. Slow, but helps avoid HTTP 429 rate-limit errors.

## How To Use

### Quick Start

1. Download all files.
2. Open `index.html` locally.

Or use the hosted page:

- https://totallynotaduck.github.io/smmoscaler/

## Tutorial For Non-Geeks

1. Input your player level.
2. Input your available gold (budget).
3. Input minimum power (treat this like minimum strength).
4. Optional: enable Special Attacks if you want to factor in special attack damage.
5. Click **Find Best Gear**.

The tool shows gear suggestions that best match your inputs.

### Sorting Tips

- Sort by **Power** for strongest stats.
- Sort by **Value** for best bang-for-buck.
- Add a minimum power filter to refine searches when low-power items clutter results.

### Unavailable / Interesting Items

Some entries may be unavailable or unusual. This section is not always perfectly accurate because item logs may be outdated.

## Logging And Data

The scaler sorts and calculates using items stored in `smmoscaler-logs.json`.

- You can call item IDs with your own API key from: https://web.simple-mmo.com/p-api/home
- You can also use a provided pre-mined log file in this repository.

Note: Data is manually called via API and stored locally, so it can become outdated.

## Large Log Files

The loader supports split logs and auto-load behavior:

- Auto-loads files listed in `smmoscaler-logs.index.json`
- If no index file exists, probes common split names such as:
	- `smmoscaler-logs.part1.json`
	- `smmoscaler-logs.part2.json`

Use the splitter utility when logs get too large:

```bash
py scripts/split_logs.py
```

Splitter behavior:

- If `smmoscaler-logs.json` is 100 MB or less, keeps one file and writes an index pointing to it.
- If `smmoscaler-logs.json` is above 100 MB, writes chunk files and updates the index so the app auto-loads all chunks.

## GitHub Actions: Automatic Log Splitting And Release

For GitHub Pages hosting, the workflow can automatically:

1. Detect changes to `smmoscaler-logs.json`
2. Run `scripts/split_logs.py`
3. Create a GitHub Release with all log chunks as assets
4. Update the index file to point to release URLs
5. Commit the index back to the repository

### How It Works

1. Use the workflow at `.github/workflows/split-and-release-logs.yml`.
2. Push changes to `smmoscaler-logs.json` on `main`.
3. Workflow runs, creates a release, and updates the index.
4. App loads split logs directly from GitHub Releases.

### Multi-User Shared Hosting

- Local use: `http://localhost:8000` via `python -m http.server 8000`
- Deployed use: `https://yourname.github.io/smmoscaler/`
- Large logs are served from Release CDN to avoid GitHub's 100 MB repo file limit.

## Credits

- Winikolo for helping with logging work.
- Fluxeon for playtesting and feedback.
- Y0mu for providing database files.

## License Note

All code is free to use and distribute, but not free to sell for profit.

All item names and item icon assets belong to Galahad Creative LLC.