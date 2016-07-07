# nonogram-samples
Nonogram Puzzles (aka Picross, Hanjie, and Griddlers) samples in JSON format.

## Overview of Nonogram puzzles

Nonogram puzzles are also called Picross, Hanjie, and Griddler puzzles.  These
are logic puzzles in which cells in a grid must be colored or left blank according 
to numbers at the side of the grid to reveal a hidden picture.   A good
introduction can be found on the the [Wikipedia page](https://en.wikipedia.org/wiki/Nonogram).

These puzzles provide interesting exercises in solving problems for which brute force may not
be an answer.  For example, a single, black and white, length 20 row, with the clues "1 1 1 1"
has millions of possiblities.  Many nanogram solvers exist.

# Goals of this project

This project aspires to provide a free and easy to use set of Nonogram puzzles to test 
algorithms.  As consensus arises, the puzzles will also include difficulty rankings.

This project also hopes to be an exercise in Documentation Driven Development, where 
emphasis is on clear and concise documentation in advance of code.  Having practiced a
dozen different methods of developing code, I am experimenting with this method.  Granted,
this project will have little executable code.

# Format of the JSON data files

## JSON?

[JSON](https://en.wikipedia.org/wiki/JSON), **J**ava**S**cript **O**bject **N**otation, is a 
format providing a human readable format for transmitting data across a wide
variety of languages.   Note that JSON allows unicode but not dates, comments, 
or executable JavaScript code.   All fieldnames will be lowercase without spaces or underscore.

## Nonograms terms

A Nonogram puzzle consists of a set of cells, each initially a colorless blank, that
will be filled with colors in accordance with the clues.   The traditional Nonogram
has two *dimensions*, rows and columns; a *color range* of two, black and white; 
a *slack color* of white, which is the color not specified in clues; and a clue for
each row or column being a sequence of *hints* specifying the number of continuous
(black) cells separated by a positive number of slack color (white) cells.   The puzzle
may have no solution, a *unique* solution, or many solutions.

[ ] Add a graphic of three nanograms with terms highlighted.

## The Format In Depth

Each file represent one set of puzzles and is represented as one large dictionary with three 
top level keys:  `header`, `common`, and `puzzles`.  The `header` contains human readable 
information about the whole file.  `common` contains a dictionary of values that will be used 
across all the puzzles, e.g., black and white with one solution.   The array `puzzles` has the
rest of the data for each puzzle.

### The Header

The header dictionary contains these key/value pairs.  Each value is optional, but having
a  `header` dictionary is not.

* `name`:  A short human name for whole file.  It should be under 60 characters and will be 
   used when displaying lists of available files.   For example, 
   "Unsolvable 5x5 black & white puzzles".  There is no requirement to be unique.
* `description`:  A longer human name for the whole file.   It can be any reasonable length 
   and the format does not care if it Markdown.
* `authors` or `author`:   One or more authors.  If there are multiple authors, use the keyword `authors` with
  the value being an array of strings.   An author string is usually "Firstname Lastname <myaddress@email.com>"
  or "Firstname Lastname (https://myhomepage.com)"
* Any other fields, including `version`, can be added and may displayed to the user.

### The Common block

Most sets of puzzles will have common attributes.  For example, a set of traditional Nonograms would
be two dimensions, a color set of black and white with white being the slack color, and each puzzle
would have a single solution.   Rather than repeat this information in each puzzle, the `common`
dictionary holds these key/value pairs.  It is an error for a puzzle to repeat or override a field
in the common block.

### The Puzzles


The `puzzles` field contains an array of dictionary.  Each puzzle is one item in the array.  It, or the 
common block, must have these fields:

* `sizes`:  An array of integers showing the maximum size of the puzzle as [an n-dimensional rectange](https://en.wikipedia.org/wiki/Hyperrectangle).   For two dimensional shapes, this is number of rows then number of columns.
* `colors`:  A string listing single characters for each available color, with the first character being the _slack color_.  These color characters may be used in the `clues`, `colormap`, and `solution` fields.
* `clues`:  Hints in a matrix; a somewhat complicated structure.
   Each *hint* is a tuple in multi-color puzzles.   The first item in the tuple is a character for the color while the second is the number of continguous squares.  For black and white puzzles, the hint may just be an integer for the number of black squares.  

   A single *clue* is a list of *hints*.  These clues are arranged in [row-major](https://en.wikipedia.org/wiki/Row-major_order) order, and for all the dimensions, in order.  For example, a 3x5 puzzle 
   (3 rows, 5 columns) would be a list of two sublists: 
      * First list would be for rows, 3 long, with clues for each of the 3 rows
      * Second list would be for columns, 5 long, with clues for each of the 5 rows
      
      [ ] Make a graphic here.
      [ ] Make a graphic or description for a three dimensional picross.


These fields are optional for each puzzle:

* `title`:   A human readable title suitable for displaying to the user, e.g., "Umbrella".  It should be under 15 characers.
* `comment`:  A comment for programmers looking deeply at this puzzle.  For example, "This is the example from figure 1.6 of my thesis."
* `numbersolutions`:  An integer showing the number of possible solutions to this puzzle.  Zero means unsolvable, one implies a unique solution, and higher numbers are ambiguous.
* `colormap`:  A dictionary mapping characters in colors to display colors.   Each key will be a single character and each value will be an rgb string in the form of `#rgb` or `#rrggbb`.
* `solution` or `solutions`:  One or more solutions to the puzzle as strings.  These will be a set of strings, in row-major order, for all solutions to the puzzle.
* Other fields such as `difficulty` or `rating` may be used, but these have no meanings as of this time.

## Examples With Explanations

[ ] Todo
