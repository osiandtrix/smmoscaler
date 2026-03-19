# Alpha's SimpleMMO Scaler (A.S.S.) and Dataminer
Made with love by Raven (Alpha, 28790)

A dedicated tool for SimpleMMO, an old-school browser MMORPG. (https://web.simple-mmo.com)


Tells you what the best item you can get for your level, and gold for the webgame SimpleMMO.
https://totallynotaduck.github.io/smmoscaler/


Uses datamined logsheet of every possible item in the game, tool included in the webpage.


Dataminer runs at 1 request per 2 seconds. Slow but you would not get HTTP429.

HOW TO USE:
Local:Download all files and run index.html

Or

Use page above.

Logging: The scaler is a calculator/sorter that sorts by the logged items in the smmoscaler-logs.json file. 
Mine items with your own APIkey from https://web.simple-mmo.com/p-api/home, and download results...

or

Download a pre-mined log file provided already in the files :)
NOTE: Since the data is MINED and stored to a log file MANUALLY, they may become outdated. 

Large log files:
- The loader now supports multi-file logs and will auto-load all files listed in smmoscaler-logs.index.json.
- If no index file exists, it also probes common split names (for example smmoscaler-logs.part1.json, smmoscaler-logs.part2.json, ...).
- Use the splitter utility to keep logs GitHub-safe when they grow too large:

```bash
py scripts/split_logs.py
```

- Behavior of splitter:
- If smmoscaler-logs.json is 100 MB or less, it keeps a single file and writes smmoscaler-logs.index.json pointing to that file.
- If smmoscaler-logs.json exceeds 100 MB, it writes chunk files and updates smmoscaler-logs.index.json so the app auto-loads all chunks.

### GitHub Actions: Automatic Log Splitting & Release

For teams hosting on GitHub Pages, a workflow is included that automatically:
1. Detects changes to `smmoscaler-logs.json`
2. Runs the split_logs.py script
3. Creates a GitHub Release with all log chunks as downloadable assets
4. Updates the index file to point to the release URLs
5. Commits the index back to the repository

**How it works:**
- Place this workflow (already in `.github/workflows/split-and-release-logs.yml`)
- Push changes to `smmoscaler-logs.json` to the `main` branch
- Workflow automatically runs, creates a release, and updates the index
- The app will load split log files directly from GitHub releases

**For multi-user shared hosting:**
- Everyone uses `http://localhost:8000` locally (with Python: `python -m http.server 8000`)
- When deployed, users access via `https://yourname.github.io/smmoscaler/`
- Large logs are served from Release CDN (no 100 MB GitHub limit issues)

Special thanks to Winikolo for helping out with the logging work uwu

Thanks to Fluxeon for playtesting the tool and providing feedback.

Thanks to Y0mu for providing database files.

All code is free to use, free to distribute, but not free to sell and profit.
All the names of the items and icons of the output items belong to Galahad Creative LLC.