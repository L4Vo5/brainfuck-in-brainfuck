# Brainfuck in Brainfuck
A brainfuck interpreter hand written in brainfuck, in only 788 instructions.

This has been done before, but mine seems to be among the shortest. [This one](https://brainfuck.org/dbfi.b) is notably much shorter.

## Usage / Limitations
Input should be given as a zero-terminated string of valid brainfuck code. Any further input past the zero will be given as input to the interpreted program, when it requests it.

Interpreted programs can't have more than 255 levels of [] nesting (or whatever the max value of a cell is in the underlying interpreter).

When interpreting the input, going left while on the first cell will result in a noop (removing this behaviour could shave off a few instructions).

Going right while on the last cell is, I think, pretty much guaranteed to break everything no matter what.

The space taken by the interpreter is twice as many cells as there are "clean" instructions in the input program (so ignoring invalid characters / comments), plus four. Then, the remaining space is halved. So on a 30k cell implementation, a 500 instruction program will have (30000 - (500 * 2) - 4) / 2 = 14498 cells to work with.

## Files
`brainfuck.txt` contains the commented code that I worked on as I developed it. It's possible some of the comments are wrong or outdated, but I hope not.

`brainfuck-clean.txt` contains only the 788 instructions of the interpreter (plus a line break at the end. oops). I removed the initial instructions used for comments, and the two optional instructions at the end.

## Notes

The interpreter can run itself multiple times over on a 30k cell implementation. The second layer will have 14210 cells to work with. The third would have 6315, the fourth 2367 (actually 2367.5, but what would half a cell look like!?), and the fifth 393 (.5), which could run a fair amount of short basic programs. I haven't actually *tried* taking it that far, though, because it'd be nightmarishly slow.

Overall, it was a fun challenge. I haven't looked too deeply into the brainfuck community, so I had to discover/rediscover many techniques on my own. This was my second brainfuck program, after this one which prints a 3 digit number: `[->+>+>+----------[<->++++++++++[->+<]]>[-<+>]<<----------[<->++++++++++[->>+<<]]>>[-<<+>>]<<<<]++++++++++++++++++++++++++++++++++++++++++++++++[->+>+>+<<<]>.>.>.<<<`.

In particular, since this program can be stacked on itself for arbitrary slowness, it was mainly an excuse to get a slow brainfuck program, as an excuse to improve the _actual_ brainfuck interpreter I'm working on, as an excuse to learn Common Lisp with an interesting but low stakes project.


Faster self-interpreters have been made, particularly by analyzing and optimizing the input. Shorter ones have been made, too. I think these two other niches sound interesting to explore in the future:
1. Being as space efficient as possible. That is, lowering the `* 2` or `/ 2` in the space formula, such that the interpreted program has as many cells as possible to operate on.
2. Being as self-stackable as possible. That's a balancing act of improving space efficiency but also keeping the program as short as possible. Some sort of perfectly self-stackable implementation might be possible, by recognizing that the input is itself and then skipping it entirely. That's kind of cheating, but it would be interesting too.
