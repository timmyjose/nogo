[![Build Status](https://travis-ci.org/timmyjose/nogo.svg?branch=master)](https://travis-ci.org/timmyjose/nogo)

A simple clone of the Atari Go game.

This game is based on The University of Queensland's School of Information Technology and Electrical Engineering
course CSSE2310/CSSE7231 course assignment.


## How to play the game?

There are two players (either human or automated) represented by board pieces 0's and X's respectively. The rules are
quite simply as follows:

  * A group of similar pieces is considered to be a string when they are all horizontally or vertically connected.
  * An empty cell horizontal or vertical to a string is considered a "liberty", or space into which the string can grow.
  * When a string has no liberties left, the string is considered to be captured.
  * The player whose string (any string) gets captured is considered to have lost the game.
  * In the case of a move which could result in either player's string(s) getting captured, the player who has the
    current move gets the option of choosing the winning move.

At each step of the game, the player (human or computer) will enter the `row` and `column` of the next move (that is, where to
place the next piece in). Only a valid move will be accepted. Also note that the user must enter the `row` and `column` values
using normal 0-based indexing counting down from the top-left of the board. For instance, move `1 2` refers to the second row, third column (the top-left position of the board has coordinates `0 0`)



## Usage

If running using Cargo,

```
$ cargo run nogo [ p1type p2type height width | filename ]
```

where `p1type` and `p2type` can be `c` (computer) or `h` (human).

`height` and `width` representing the size of the board represented as cells must be integrs between 4 and 1000 inclusive.

`filename` refers to the full path of a previously saved game. The game will continue from where it left off, with the same player types as inferred from the saved game data.

If running using the executable directly,

```
$ nogo [ p1type p2type height width | filename ]
```

All terms have the same exact meaning as explained previously.



## Saving/Loading a game

At any point in time during gameplay, instead of entering the row and column of the next move, the player can enter `w[full-path-of-the-save-file]`. That is, `w` followed immediately by the full path of the file to save the game to with no spaces in between. For example:

```
Player X> w/opt/games/my_save_file.nogo
```

This, of course, means that for a game to be saved during play, at least one of the two players must be a human player.

To load a saved game file, simply invoke it as shown in the `Usage` section:

```
$ cargo run nogo /opt/games/my_save_file.nogo
```

for instance. The game will pick up from where it left off.


## Sample gameplay

To assist in getting started out with the game, here is a small gameplay between a human (player 1) and the computer (player 2).

```
$ cargo run c h 5 5
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/nogo c h 5 5`
Welcome to nogo!

/-----\
|.....|
|.....|
|.....|
|.....|
|.....|
\-----/

Player 0: 2 0
/-----\
|.....|
|.....|
|0....|
|.....|
|.....|
\-----/

Player X> 0 1
/-----\
|.X...|
|.....|
|0....|
|.....|
|.....|
\-----/

Player 0: 4 1
/-----\
|.X...|
|.....|
|0....|
|.....|
|.0...|
\-----/

Player X> 2 1
/-----\
|.X...|
|.....|
|0X...|
|.....|
|.0...|
\-----/

Player 0: 0 2
/-----\
|.X0..|
|.....|
|0X...|
|.....|
|.0...|
\-----/

Player X> 1 0
/-----\
|.X0..|
|X....|
|0X...|
|.....|
|.0...|
\-----/

Player 0: 2 3
/-----\
|.X0..|
|X....|
|0X.0.|
|.....|
|.0...|
\-----/

Player X> 3 0
/-----\
|.X0..|
|X....|
|0X.0.|
|X....|
|.0...|
\-----/

Player X wins!

Thank you for playing nogo!
```

Another example, this time with computer playing against computer:

```
$ cargo run c c 7 5
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/nogo c c 7 5`
Welcome to nogo!

/-----\
|.....|
|.....|
|.....|
|.....|
|.....|
|.....|
|.....|
\-----/

Player 0: 2 0
/-----\
|.....|
|.....|
|0....|
|.....|
|.....|
|.....|
|.....|
\-----/

Player X: 3 1
/-----\
|.....|
|.....|
|0....|
|.X...|
|.....|
|.....|
|.....|
\-----/

Player 0: 4 1
/-----\
|.....|
|.....|
|0....|
|.X...|
|.0...|
|.....|
|.....|
\-----/

Player X: 5 2
/-----\
|.....|
|.....|
|0....|
|.X...|
|.0...|
|..X..|
|.....|
\-----/

Player 0: 5 1
/-----\
|.....|
|.....|
|0....|
|.X...|
|.0...|
|.0X..|
|.....|
\-----/

Player X: 6 2
/-----\
|.....|
|.....|
|0....|
|.X...|
|.0...|
|.0X..|
|..X..|
\-----/

Player 0: 0 3
/-----\
|...0.|
|.....|
|0....|
|.X...|
|.0...|
|.0X..|
|..X..|
\-----/

Player X: 6 3
/-----\
|...0.|
|.....|
|0....|
|.X...|
|.0...|
|.0X..|
|..XX.|
\-----/

Player 0: 1 4
/-----\
|...0.|
|....0|
|0....|
|.X...|
|.0...|
|.0X..|
|..XX.|
\-----/

Player X: 0 2
/-----\
|..X0.|
|....0|
|0....|
|.X...|
|.0...|
|.0X..|
|..XX.|
\-----/

Player 0: 3 0
/-----\
|..X0.|
|....0|
|0....|
|0X...|
|.0...|
|.0X..|
|..XX.|
\-----/

Player X: 1 3
/-----\
|..X0.|
|...X0|
|0....|
|0X...|
|.0...|
|.0X..|
|..XX.|
\-----/

Player 0: 4 0
/-----\
|..X0.|
|...X0|
|0....|
|0X...|
|00...|
|.0X..|
|..XX.|
\-----/

Player X: 3 4
/-----\
|..X0.|
|...X0|
|0....|
|0X..X|
|00...|
|.0X..|
|..XX.|
\-----/

Player 0: 2 4
/-----\
|..X0.|
|...X0|
|0...0|
|0X..X|
|00...|
|.0X..|
|..XX.|
\-----/

Player X: 4 4
/-----\
|..X0.|
|...X0|
|0...0|
|0X..X|
|00..X|
|.0X..|
|..XX.|
\-----/

Player 0: 2 3
/-----\
|..X0.|
|...X0|
|0..00|
|0X..X|
|00..X|
|.0X..|
|..XX.|
\-----/

Player X: 6 1
/-----\
|..X0.|
|...X0|
|0..00|
|0X..X|
|00..X|
|.0X..|
|.XXX.|
\-----/

Player 0: 1 2
/-----\
|..X0.|
|..0X0|
|0..00|
|0X..X|
|00..X|
|.0X..|
|.XXX.|
\-----/

/-----\
|..X0.|
|..0X0|
|0..00|
|0X..X|
|00..X|
|.0X..|
|.XXX.|
\-----/

Player 0 wins!

Thank you for playing nogo!
```

An example of saving the game during play, and then loading it again:

```
$ cargo run c h 5 5
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/nogo c h 5 5`
Welcome to nogo!

/-----\
|.....|
|.....|
|.....|
|.....|
|.....|
\-----/

Player 0: 2 0
/-----\
|.....|
|.....|
|0....|
|.....|
|.....|
\-----/

Player X> 1 0
/-----\
|.....|
|X....|
|0....|
|.....|
|.....|
\-----/

Player 0: 4 1
/-----\
|.....|
|X....|
|0....|
|.....|
|.0...|
\-----/

Player X> 3 1
/-----\
|.....|
|X....|
|0....|
|.X...|
|.0...|
\-----/

Player 0: 0 1
/-----\
|.0...|
|X....|
|0....|
|.X...|
|.0...|
\-----/

Player X> 3 0
/-----\
|.0...|
|X....|
|0....|
|XX...|
|.0...|
\-----/

Player 0: 0 2
/-----\
|.00..|
|X....|
|0....|
|XX...|
|.0...|
\-----/

Player X> wsave_file.gm

Finished saving current game state to file save_file.gm

Thank you for playing nogo!

$ cargo run save_file.gm
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/nogo save_file.gm`
Welcome to nogo again!

/-----\
|.00..|
|X....|
|0....|
|XX...|
|.0...|
\-----/

Player X> 2 1
/-----\
|.00..|
|X....|
|0X...|
|XX...|
|.0...|
\-----/

/-----\
|.00..|
|X....|
|0X...|
|XX...|
|.0...|
\-----/

Player X wins!

Thank you for playing nogo!
```


