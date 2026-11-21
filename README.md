# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/abilyusa/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/abilyusa/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4 KB of Python. It plays the house gauntlet through the
env at `MAKEFUN_ENV_URL` and searches to a fixed node budget, never a clock,
so every trial replays move for move.

## The engine

`main.py` is the whole engine, packed with `makefun compress` from the
readable source the bundle carries beside the transcripts. Inside:

- 0x88 board, alpha-beta with iterative deepening to a fixed node budget
  (60,000 nodes a move, tapered late in long games)
- Quiescence over captures and promotions, and over every reply to a check
- Transposition table, killer moves, MVV-LVA ordering, late-move reductions
  and null-move pruning
- Evaluation: material plus piece-square tables (middlegame and endgame king
  tables), the bishop pair; a repetition inside the search scores 0

Python 3.13, standard library only. It reads no file but itself, calls no
model and reaches no network but the env.

## Grade it locally

From the competition kit, with Docker:

    node cli/makefun.mjs grade-local --kit . --bot <this repository> --driver docker

It plays one practice trial (6 games, depth-2 to nodes-500k) and replays it.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
