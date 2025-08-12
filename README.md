# Brainfuck in Brainfuck
A brainfuck interpreter written in brainfuck, in only 791 instructions.

This has been done before, but I couldn't find any that were this short. To be fair, I did not do much digging.

## Usage
Input should be given as a zero-terminated string of valid brainfuck code. Any further input past the zero will be given as input to the interpreted program, when it requests it.

When interpreting the input, going left while on the first cell will result in a noop.

Interpreted programs can't have more than 255 levels of [] nesting (or whatever the max value of a cell is in the underlying interpreter).

## Limitations / Characteristics
Obviously, this interpreter is *really* slow. But it should be able to run itself multiple times over.

The space taken by the interpreter is twice as many cells as there are "clean" instructions in the input program (so ignoring invalid characters), plus five. Then, the remaining space is halved. So on a 30k cell implementation, a 500 instruction program will have (30000 - (500 * 2)) / 2 = 14500 cells to work with.

So, it can run itself, and the second layer will have 14209 cells to work with. The third would have 6313, the fourth 2365, and the fifth 391, which could run a fair amount of short basic programs. I haven't actually *tried* taking it that far, though, because it'd be nightmarishly slow. If you do nest it, please use the clean version, as it'll be much faster to load in and also has no extraneous instructions at the start.

## Files
`brainfuck.txt` contains the commented code that I worked on as I developed it. It's possible some of the comments are wrong or outdated, but I hope not.

`brainfuck-clean.txt` contains only the 791 instructions of the interpreter (plus a line break at the end. oops).
