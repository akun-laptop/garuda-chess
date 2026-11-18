# garuda-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/akun-laptop/garuda-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/akun-laptop/garuda-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Garuda — a deterministic 4 KB Python chess engine (stdlib only): 0x88 board, alpha-beta with null-move pruning and late-move reductions under a fixed 60,000-node budget per move. Mean practice Elo 1,669, about +300 over the Sunfish-4K house baseline.

## Run it

```sh
MAKEFUN_ENV_URL=http://localhost:8080 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=t2vhhcmm&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>

## How it plays

- **0x88 board**, pseudo-legal move generation with a make/unmake legality filter.
- **Alpha-beta + iterative deepening** under a fixed 60,000-node budget per move — no clocks, so a replayed game produces the exact same moves.
- **Null-move pruning** (R=2), **late-move reductions**, transposition table with mate-distance adjustment, two killers per ply, MVV-LVA ordering, quiescence over captures, promotions, and all evasions in check.
- **Eval**: material + piece-square tables, tapered king safety, bishop pair, pawn structure (doubled, isolated, passed pawns), king pawn shield, rooks on open files, tempo.
- **Repetition awareness**: replays the game history, scores repeats as draws.

## Results (practice gauntlet, 6 games each — final v3)

| trial | result | Elo |
|-------|--------|-----|
| trial-0 | 5W–0D–1L | 1,654 |
| trial-1 | 5W–1D–0L | 1,809 |
| trial-2 | 4W–1D–1L | 1,545 |
| **mean** | **14W–2D–2L** | **1,669** |

House baseline (Sunfish-4K) averages ~1,365 Elo on the same trials. Named after the Garuda, the mythical bird of Indonesian legend — fast, sharp-eyed, and it never blinks.

## Build

The readable source is `source.py` (kept uncommitted, beside the entry). Packed with the kit's own compressor only:

```
node <kit>/cli/makefun.mjs compress source.py --out main.py
```

## License

MIT — see `LICENSE`.
