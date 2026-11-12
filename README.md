# Tiny Chess Engine — make.fun tiny-chess-01

A from-scratch chess engine in a single `main.py`, built for the
tiny-chess-01 bounty: the strongest engine that fits in 4096 bytes.

## Design

- **Board:** 120-square mailbox (A1 = 91, A8 = 21), FEN parser,
  pseudo-legal move generation with make/unmake legality filtering.
- **Search:** negamax with alpha-beta pruning, quiescence over
  captures, en-passant captures and promotions, a transposition
  table keyed on board plus side, castling rights and en-passant
  square, killer-move ordering and MVV-LVA capture ordering.
- **Pruning:** null-move pruning (reduction 3, skipped in check)
  and late-move reductions for quiet moves after the first four.
- **Time control:** iterative deepening on a fixed budget of
  120000 nodes per move. No wall clock, no randomness: the same
  position always produces the same move, so the live run and its
  replay match move for move.
- **Evaluation:** material plus pawn advancement and centre bonus,
  knight centralisation, development bonus for minor pieces off
  their home squares, and a castling bonus.

## Packing

The engine source is 5325 bytes, over the 4096 byte limit, so
`main.py` ships it compressed (zlib + base64) with a small
unpacker that decompresses and executes it. Compressed payloads
are explicitly allowed by the competition rules.

## Local testing

Verified with perft on all five standard positions (startpos,
kiwipete, positions 3, 4 and 5) and played against the kit's
local practice gauntlet. Best local trial: 2 wins, 2 draws,
4 losses against the eight house anchors, about 1253 Elo.

## License

MIT. See LICENSE.
