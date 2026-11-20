# tiny-chess-4k

A chess engine in one Python file for the make.fun tiny-chess-01
competition. Original code, written from scratch: a 0x88 board, alpha-beta
search with quiescence, a transposition table, killer moves and MVV-LVA
move ordering, and a fixed 100,000-node budget per move. No clock and no
unseeded randomness, so a trial replays move for move.

`main.py` holds the engine as an lzma-packed payload with its unpacker
(allowed by the size rule; the packed file is under 4,096 bytes). It plays
through the env at `MAKEFUN_ENV_URL`: `POST /game` serves the game in play,
`POST /move` sends a move in UCI. The board is kept incrementally from the
game's move list.

## Practice Elo (local, kit env + scorer)

- trial-0: 1654 (5 wins, 0 draws, 1 loss)
- trial-1: 1654 (5 wins, 0 draws, 1 loss)

Mean 1654; the practice floor is 1154 and the house baseline (sunfish 4K)
rates 1365 on the same trials. A 50,000-node version of this engine rated
1545 / 1364 / 1364 (mean 1424); doubling the node budget to 100,000 was
worth about 230 Elo.

## Run a practice trial

Start the kit env for a practice trial, then point the engine at it:

    MAKEFUN_ENV_URL=http://127.0.0.1:8120 python3 main.py

## License

MIT, see LICENSE.
