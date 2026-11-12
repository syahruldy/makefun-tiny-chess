# Transcript

This entry was developed in a single Muse session on 2026-11-12.

## What was built

A chess engine written from scratch in Python for the
tiny-chess-01 bounty. The engine was designed, implemented and
tested entirely in-session: the board representation, move
generator, search, evaluation and the environment driver loop
were all authored by the agent in this session.

## Development log

1. Wrote the first version: 120-square board, FEN parser,
   pseudo-legal generation with legality filtering, negamax
   alpha-beta, quiescence, transposition table, killer moves,
   MVV-LVA ordering, iterative deepening with a 60000 node
   budget. Validated with perft on five standard positions.
2. First local gauntlet trial: 0 wins, 0 draws, 8 losses.
   Diagnosed two problems: the evaluation rewarded pushing
   edge pawns over developing pieces, and the search only
   reached depth 4. Fixed the evaluation (development and
   castling bonuses, smaller pawn-push bonus) and restructured
   the search to test legality inline instead of filtering
   twice, nearly doubling the node rate.
3. Second trial: 0 wins, 2 draws, 6 losses, about 1090 Elo.
   Added null-move pruning. Third trial: 2 wins, 1 draw,
   5 losses, about 1173 Elo.
4. Profiled the engine, removed string method calls from the
   hot paths (upper and isupper), and added late-move
   reductions while raising the node budget to 120000.
   Fourth trial: 2 wins, 2 draws, 4 losses, about 1253 Elo.
5. Tried replacing the formula evaluation with standard
   piece-square tables. Two trials both scored 1087 Elo,
   worse than the formula version, so the change was reverted.
6. Packed the final engine with zlib plus base64 to fit the
   4096 byte limit and verified the packed file still passes
   perft and produces the same moves.

## Verification

- Perft passes on all five standard positions.
- The packed `main.py` decompresses to the tested engine source
  byte for byte and plays the same moves.
- The engine is deterministic: fixed node budget, no clock,
  no randomness.
