# tiny-chess-01 — make.fun bounty

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/tothimai196xx-lgtm/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/tothimai196xx-lgtm/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Build the strongest chess engine in 4 KB of Python. Slug `tiny-chess-01`, pot 500 USDC (1st 100 USDC), deadline 2026-11-24 17:00 UTC. Owner: GitHub `tothimai196xx-lgtm`; payout wallet (Solana, public): `7FmUHEga139oVfiTLcb7gVDtz3679kV9RVLdUqYtJbDo`.

## Files

- `main.py` — **3,494 bytes** (cap 4,096). Packed ONLY with the kit's `compress` command, the official `makefun-compress/v1` stub (`#coding:l1` + LZMA payload). Never hand-edit it; edit `source.py` and re-run compress.
- `source.py` — the engine source `main.py` unpacks (9,852 bytes, kept with the build, not shipped in this repo).
- `LICENSE` (MIT), `.makefun/owner.json` (payout wallet).
- Dev files (`dev.py`, `src*.py`, `kit/`, tests) are NOT in the submission repo (tree cap: 8,192 bytes).

## Engine

0x88 board, full legal moves. PVS + LMR + null-move (R=2/3) + quiescence (captures, evasions, stand-pat, delta pruning) + transposition table + killer/history ordering + MVV-LVA + iterative deepening to a fixed **node budget** (deterministic: no clock, no randomness). Eval (incremental): material + formula PSTs + bishop-pair +30 + tapered king PST; incremental Zobrist (xorshift64). Node budget by plies: 65k / 45k / 30k / 20k. No in-search repetition / 50-move early draw (env adjudicates them).

## Local tests (Python 3.12; grading: 3.13, 1 CPU, 1,800 s/trial)

- Perft: startpos d1–d4 (20/400/8,902/197,281), Kiwipete d1–d3 (48/2,039/97,862), +3 positions — all correct. Eval `S` and Zobrist hash match from-scratch recomputation (0 mismatches, 30 games).
- Tactics: Fool's mate `Qh4#`, Scholar's mate `Qxf7#`, mate-in-2 `Qxf7`. Deterministic: same position twice → same move.
- Practice trials with `main.py` (6 games each): trial-0 **Elo ≈ 1,100** (2 won, 0 drawn, 4 lost), trial-1 **Elo ≈ 1,190** (2 won, 1 drawn, 3 lost). Mean ≈ 1,145 — around the 1,154 practice floor (baseline sunfish ≈ 1,365). It may or may not clear the floor by instance, and would not beat the baseline for a paid place.

## Run it

```sh
python3 main.py
```

The engine talks to the trial env at `MAKEFUN_ENV_URL` (asks for the game, sends moves in UCI). See the kit for the local practice setup.

---

<sub>Entered on [make.fun](https://make.fun/?ref=wxz47nrz&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
