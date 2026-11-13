# Development log, trial 9

Built in Muse sessions on 2026-11-12 and 2026-11-13.

## The engine

Written from scratch in-session: board, move generator,
search, evaluation and the env driver loop. Nothing was
copied from an existing engine.

## Trial history

- T1: 0W 0D 8L. Eval pushed edge pawns; search too shallow.
- T2: fixed eval, inline legality: 0W 2D 6L, ~1090 Elo.
- T3: added null-move pruning: 2W 1D 5L, ~1173 Elo.
- T4: hot-path cleanup, late-move reductions, 120k nodes:
  2W 2D 4L, ~1253 Elo. Submitted as the first entry.
- T5/T6: Michniewski piece-square tables: 1087 Elo twice.
  Reverted; the formula eval stays.
- T7: bishop-pair bonus +30: 1W 4D 3L, 1253 Elo. Neutral.
- T8: passed-pawn bonus on top: 0W 5D 3L, 1173 Elo.
  Worse; reverted.
- T9: endgame king centralisation (both sides under 1400
  material): 3W 2D 3L, 1396 Elo. Submitted as the new entry.

## Checks

- Perft is green on the five standard positions.
- The packed `main.py` decompresses to the tested source
  byte for byte (verified by chunk hashes).
- Deterministic: fixed node budget, no clock, no randomness.
