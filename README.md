Battleship-Game-Using-C-with-FIFO

Built a two-player terminal-based Battleship game in C using FIFOs (named pipes) for inter-process communication between a server and two client processes. Implemented features like ship placement, attack/defense logic, hit/miss detection, bonus turns, scoring system, and real-time board display with ANSI color formatting.
Gained hands-on experience with Unix system calls (read, write, open), process synchronization, and low-level IPC mechanisms in Linux.

Introduction
This project implements a two-player Battleship game in C, running on a Linux system with two separate
terminal windows, one for each player. Each player places five ships on a 10×10 grid. To ensure fairness, the
system implements a fog-of-war mechanism that hides both the player's own ship placement and the
opponent's ships. They only see hits, misses, and scores, making the game suitable for split-screen play on
the same machine without cheating. Victory is achieved in two possible ways:
 Sink all enemy ships, or
 Reach 17 points (1 point per ship hit + bonus/penalty cells). Cells/Ships are placed as:
 Bonus Cell (1 cell, +5 points)
 Penalty Cell (1 cell, +2 of opponent)
 Carrier Ship (5 cells/points)
 Battleship (4 cells/points)
 Destroyer Ship (3 cells/points)
 Submarine (3 cells/points)
 Patrol Boat (2 cells/points). Methodology
The project will be developed in C for Linux, utilizing a client-server architecture with Inter-Process
Communication (IPC) for split-terminal gameplay. The methodology is structured into distinct phases:
Core Architecture & Process Creation: A central server process will be forked to manage the game state, rules, and scoring. It will create two client processes (Player 1 and Player 2), each attached to a separate
terminal window. This ensures isolated views and enforces the fog-of-war.
Game State & Grid Management: The server will maintain two private 10x10 grids per player (one for
ship placement, one for tracking hits/misses on the opponent). Dynamic memory allocation (malloc) will be
used for grid structures. Ship placement will be validated for boundaries and overlaps during setup. Inter-Process Communication (IPC): Named Pipes (FIFOs) or Message Queues will be established for
bidirectional communication between the server and each client. This will handle turn synchronization, coordinate transmission, and result broadcasting. Semaphores or mutexes will manage critical sections to
prevent race conditions during score updates and turn switching. Fog-of-War & UI Implementation: Each client process will only receive and display a "view" grid from
the server, where:
 ~ represents unknown water.  O represents a miss.  X represents a hit. The player's own ships and the opponent's un-hit ships remain hidden. A simple text-based UI will be built
using ANSI escape codes for grid display, score, and turn prompts. Game Logic & Scoring Engine: The server will validate all moves, check for hits/misses, and apply
scoring rules:
 Standard hit: +1 point.  Bonus cell hit: +5 points.  Penalty cell hit: Awards +2 points to the opponent. Sinking a ship (all cells hit) triggers a notification. The game ends when either all ships of one player are
sunk or any player’s score reaches/ exceeds 17 points. Integration & Testing: Components will be integrated incrementally. Testing will focus on IPC reliability, correct fog-of-war rendering, accurate score calculation, and robust handling of invalid inputs. Scope
In-Scope:
 A fully functional two-player Battleship game played on a single Linux machine via two terminals.  Correct implementation of all five ship types, one bonus cell, and one penalty cell per player.  A working fog-of-war system where players only see hits, misses, and scores.  A turn-based system with enforced synchronization.  Dual victory conditions: destroy all opponent’s ships OR reach 17 points first.  A text-based interface with clear grid visualization and game status.  Proper memory management and cleanup of all processes and IPC resources. Out-of-Scope:
 Graphical User Interface (GUI) beyond terminal-based text.  Network play over different machines.  AI opponents or single-player mode.  Saving and loading game states.  Advanced animations or sound effects.  Variable grid sizes or configurable ship sets beyond the specified five.
