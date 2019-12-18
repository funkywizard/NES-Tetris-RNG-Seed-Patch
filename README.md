# NES-Tetris-RNG-Seed-Patch
Patch for NES Tetris Rom to allow for playing the game with the same pieces multiple times, using a seed value 000 - 999

On the A-Type Level Select screen, hit "select" while highlighting a specific level (0 - 9) to enter that digit into the seed value. Repeat until you have your desired 3 digit seed value stored. Seed "850" is especially challenging.

Patch uses a 256 entry lookup table at memory location D800 - D8FF to iterate the RNG function "X" number of times for each new piece, with X chosen by the value in the table, and your position in the table. Seed value chosen determines your initial starting place in the lookup table, as well as, how many entries are skipped in the lookup table after each piece is dealt.

"skip values" 0 - 9 correspond to the first 10 prime numbers (1 / 3 / 5 / 7 / 11 / 13 / 17 / 19 / 23 / 29), indicating how many entries in the table will be skipped after each piece selection. When entry 256 is exceeded, it wraps around to the start of the table again.

Starting location in the 256 entry lookup table is entered as a two digit number 00 - 99. This is converted to hex, so, hex values 00 - 09, 10 - 19, 20 - 29, etc. are available. A further improvement to the UI is possible to allow for the full 00 - FF range of starting values, but the current design was simpler to implement and seemed sufficient.

If you'd like to change the lookup table, for example, for competitive play where you don't want players to have memorized the piece sequence for a given seed value, you can edit the 256 bytes D800 - D8FF. Currently, this has values 10 - 99, converted to hex, so, hex values 10 - 19, 20 - 29, 30 - 39, etc, giving 90 possible number of times to iterate the RNG for each piece. It would be possible to change this to 00 - FF, for 256 possible times to iterate the RNG function for each piece. However, it is recommended not to use small numbers of iterations, so starting at hex 10 (decimal 16) is reasonable.
