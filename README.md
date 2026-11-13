# tiny-chess-01 entry: trial-9 engine

A scratch-built chess engine in one `main.py`, squeezed into
4096 bytes for the tiny-chess-01 bounty.

## How it plays

- **Board:** 120-square mailbox, A1 at 91 and A8 at 21, with a
  FEN reader and pseudo-legal generation plus make/unmake
  legality checks.
- **Search:** negamax alpha-beta, quiescence over captures,
  en-passant takes and promotions, transposition table keyed
  on position, side, castling and en-passant, killer moves
  and MVV-LVA ordering for captures.
- **Pruning:** null-move pruning at reduction 3 (never in
  check) and late-move reductions on quiet moves past the
  first four.
- **Budget:** iterative deepening capped at 120000 nodes per
  move. No clock, no random numbers: a position always yields
  the same move, so live play and replay agree.
- **Evaluation:** material, pawn advance and centre, knight
  centralisation, development and castling, a bishop-pair
  bonus, and king centralisation in the endgame.

## Packing

The source is 5626 bytes, past the limit, so `main.py`
carries it zlib-compressed and base64-encoded with a tiny
unpacker. The rules allow compressed payloads.

## Local trials

Perft is green on the five standard positions. Trial 9 on the
kit practice gauntlet: 3 wins, 2 draws, 3 losses, 1396 Elo —
above the 1325 house baseline mean. Earlier trials: bishop
pair alone 1253, passed-pawn bonus 1173 (reverted).

## License

MIT, see LICENSE.
