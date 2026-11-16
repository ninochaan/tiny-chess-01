# tiny-chess-01 entry

An original chess engine in a single `main.py` of at most 4,096 bytes
(Python 3.13, standard library only).

Design: 0x88 board, negamax alpha-beta with principal-variation search,
transposition table, quiescence search (captures, promotions, check
evasions), check extensions, killer-move ordering, and a material +
piece-square-table evaluation. Deterministic: fixed 60,000-node budget
(lower than the 65,000 used in early trials, for more wall-clock margin
in the 8-game final), seeded Zobrist keys, no clock, no randomness at
run time.

Build: the engine is developed as a readable source file, `engine.py`,
and the shipped `main.py` (3,293 bytes) is produced from it with the
kit's own `makefun compress`, the makefun-compress/v1 stub around an
LZMA stream of the source, as the competition rules expressly allow.
The decompressed payload is the whole engine and runs standalone.

Local practice trials with the kit's gauntlet (6 games each, Elo on the
house anchor ladder, final-qualification bar 1,154): 1,545, 1,545 and
1,279 with the exact shipped engine — about 1,450 combined over
18 games.

It plays through the make.fun environment protocol: with
`MAKEFUN_ENV_URL` set, it polls `POST /game` and answers with
`POST /move` until the game is done.

MIT licensed — see `LICENSE`.
