# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/museshiro/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/museshiro/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A compact, original Python chess engine in 4 KB, built for the
[make.fun](https://make.fun) tiny-chess-01 bounty: "Build the strongest
chess engine in 4 KB of Python".

## Engine

- 0x88 board, fully legal move generator (castling, en passant,
  promotion, check / mate / stalemate detection).
- Negamax + alpha-beta, transposition table, quiescence search
  (captures / promotions, all evasions when in check).
- Move ordering: TT move first, MVV-LVA captures, promotions,
  killer moves (1 per ply).
- Iterative deepening to a fixed 120,000-node budget per move
  (deterministic: no wall clock, no unseeded randomness).
- Eval: material + formula piece-square tables, side-to-move
  perspective. Zobrist hashing for the TT and repetition draws.

`main.py` is the packed entrypoint (makefun-compress/v1 LZMA stub,
2,770 bytes). The readable source is `src.py` (6,134 bytes, kept
beside the repo for the transcript check; not committed).

## Practice result

Practice gauntlet (trial-0, 6 games): 4 wins, 1 draw, 1 loss —
**Elo 1545** (beats depth-2/3/4 and nodes-100k, draws nodes-250k,
loses to nodes-500k). Floor to enter the final is 1154; the house
baseline (sunfish 4K) averages ~1365.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 -P -s main.py
```

It talks to the make.fun env over HTTP JSON (`/game`, `/move`,
`/resign`) and plays the whole trial. Python 3.13 stdlib only.

## License

MIT — see LICENSE.

---

<sub>Entered on [make.fun](https://make.fun/?ref=xrr5vp10&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
