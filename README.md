# tiny-chess-v12

A chess engine in 4 KB of Python, built for the make.fun competition
**tiny-chess-01** — "Build the strongest chess engine in 4 KB of Python".

`main.py` is the whole engine (4,069 bytes as committed): a single-file
Python program that talks to the competition env over HTTP
(`MAKEFUN_ENV_URL`). The source is packed with LZMA + base85 and unpacked
at startup by a one-line loader; the engine itself is 100% fresh code
written for this competition.

## Engine

- 0x88 board, alpha-beta search with a fixed 50,000-node budget per move
  (deterministic — no wall clock in the search)
- Transposition table (move-only, keyed by the full position)
- Killer moves, null-move pruning, late-move reductions, check extension
- Quiescence search over captures, promotions and check evasions, with
  delta pruning
- Evaluation: material + procedural piece-square tables + bishop pair +
  king safety + passed-pawn bonuses (bitboard based), computed from
  scratch at the leaves

## Results (grade-local, kit practice instances)

| trial | Elo | W-D-L |
|-------|-----|-------|
| 0     | TBD | TBD   |
| 1     | TBD | TBD   |

Practice floor is 1,154. The entry that clears it plays the 8-game live
gauntlet in the final (deadline to resubmit: 25 Nov 2026).

## Reproduce the grade

Requires the tiny-chess-01 kit (practice instance 0):

```sh
# from the kit directory, with the env server + scorer (see kit README):
./grade.sh 0 main.py v12final-t0
```

`main.py` reads `MAKEFUN_ENV_URL` and plays 8 games against the house
gauntlet (depth-2/3/4 and 100k–2M-node engines), then exits.

## License

MIT — see `LICENSE` (`SPDX-License-Identifier: MIT`).
