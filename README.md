# shiny bell tracker

fan-made, read-only tracker for TMF Pass bells (The Mutual Fun). not affiliated.

- single file: `index.html` (inline css + js, no build, no backend, no wallet connect)
- chain: Robinhood Chain mainnet (chain id 4663)
- contract: TMF Pass `0xED37605FF0e513e46d50B26244DEb2024189751a`
- rpc: https://rpc.mainnet.chain.robinhood.com, fallbacks https://robinhood-rpc.publicnode.com and https://robinhood.drpc.org
- ens: reverse lookup on ethereum mainnet via the ENS Universal Resolver (publicnode / drpc)

how it works
- `bellCount()` = wallets that have rung. `hasRung(holder)` decides if a pass is shiny (same check the official pass art uses), so one ring shines every pass in that wallet.
- order + time + tx come from `BellRung(address indexed ringer, uint256 count)` logs (seeded up to a recent block, then scanned live).
- `ownerOf`, `textOf`, `sourceOf`, `tokenURI` are read in one Multicall3 call per refresh. refresh every 60s.

host it anywhere static: GitHub Pages (this folder, `.nojekyll` included), Cloudflare Pages, Netlify, etc.

verify locally
    python3 -m http.server 18431 --bind 127.0.0.1
    node test.js          # headless check vs truth.json + screenshots
    /workspace/tmf/venv/bin/python verify_truth.py   # web3 ground truth -> truth.json
