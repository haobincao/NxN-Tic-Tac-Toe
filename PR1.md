# PR1

# ***2. NxN Tic-Tac-Toe***

You will write an `n`x`n` tic-tac-toe game/program that utilizes **functions and arrays**. Please start early and DO NOT succumb to any temptation to look for solutions or share code with others.

### **Description & Requirements**

In this program, you will write a program to allow two players to play the classic game of Tic-Tac-Toe. The first player will be represented with `X`s and the second player with `O`s. In this program we will provide you a skeleton outline in `main()` and ask you to implement several functions that `main()` can call to carry-out major tasks of the game (e.g. `printTTT()`, `checkForWinner()`, and `checkForDraw()`).

You **MUST complete the 6 functions prototyped below** and fill in the necessary parts of **`main()`** to call the various functions where appropriate.

*`// High-level functions that MUST be called by main()***void** **printTTT**(**char** grid[], **int** dim);
**int** **checkForWinner**(**char** grid[], **int** dim);
**bool** **checkForDraw**(**char** grid[], **int** dim);

*// 3 small utility functions for converting 1D <=> 2D indices// These should be used wherever appropriate, but may not// all be needed.  Still, you must define them.***char** **getEntryAtRC**(**char** grid[], **int** dim, **int** r, **int** c);
**int** **idxToRow**(**int** idx);
**int** **idxToCol**(**int** idx);`

In all these functions, we pass the array (named `tttdata` in `main()` but named `grid` in all the input arguments) storing the `X`s, `O`s, and blank (`?`) spots so that the functions can examine the game state. We will use the character `?` to represent blank spots, so that the user sees they are available. Remember, arrays are passed by reference and any modification in a function is made to the original, unlike scalar values (e.g. `int`, `double`, etc.) which are passed by value. Please note that as you implement these functions, **you must follow the guidelines and produce the return values** that are specified in the comments above each prototype in the skeleton code. Those comments act as requirements just as much as this writeup. While you are free to define and use additional functions, you **must implement and use the ones defined above**.

### **Winning**

To *win*, a player must completely fill **any** row, column, or one of the *two* diagonals with their symbol (i.e. Xs or Os). **As soon as this condition occurs for any player, the program should stop and print the correct message**, either:

`X player wins!`

or

`O player wins!`

The program should then exit after printing one of these messages (and print nothing else).

### **Draws**

We want to determine if the game will end in a draw and potentially end early, declaring a draw, without needing all squares to be filled in. We will define a *draw* as having occurring when each row, column, **and** each of the two diagonals have at least one `X` and one `O`, since that would mean it is impossible for either player to win. This should be checked after each turn and, if satisfied, the game should stop and the following message should be printed:

**`Draw**...game over!`

The program should then exit after this message (and print nothing else).

**Important: While we may be able to determine a draw will occur even earlier (before one of each symbol exists in each row/column/diagonal), please just implement this algorithm as described above.**

Note: These win and draw message strings (character arrays) have been created for you in `main()` and can be output with a corresponding `cout`:

  `cout << xwins_msg << endl;  *// OR*cout << owins_msg << endl;  *// OR*cout << draw_msg << endl;`

### **Getting the skeleton**

The code has been started for you in `tttn.cpp`

### **Parts of the Program & Grid Size**

To start, you can attempt to write the code for only a **3x3** tic-tac-toe grid. But to pass several of our tests you must make your code work for a generic **`n` x `n`** tic-tac-toe grid (where `n` is an odd integer from the set `3`, `5`, `7`, `9`, or `11`). The largest grid will be `11`x`11` and thus we will need an array of at most 121 locations (this array of 121 locations is declared at the start of `main()`).

### **Grid size**

We want you to implement the `n` x `n` version (rather than just `3`x`3` version) of the program to have you practice generalizing patterns. We will use the variable name `dim` to specify `n`, which stands for the **dim**ension of one side of the square grid. And all of your code should be generalized to work for a given value of `dim`. Thus, a majority of your code will use values that are some function of `dim`.

While we allocate the `tttdata`/`grid` array for size 121 (i.e. 11x11), we will not use the entire array for smaller dimensions. The user will enter the **dim**ension via `cin` at the start of the program and then main will create the initial array contents for that size. For example, if the user enters a dimension of `3` then your could should only use entries 0 through 8 in the `tttdata`/`grid` array. **When you test your code you will always need to enter that dimension value first before the game can truly start.**

### **1D vs. 2D**

While tic-tac-toe is inherently 2 dimensional and would naturally lend itself to a 2D array, we are artificially forcing you to use a **1 dimensional** array, for several reasons:

1. We may not have fully covered multi-dimensional arrays
2. We want you to understand how higher-dimensional arrays are “linearized” to 1-dimension
3. It provides good opportunity to use functions to **abstract** implementation details such as conversion between 1D and 2D coordinates.
4. It is a good application of certain arithmetic operations required to perform the desired conversion between 1D and 2D coordinates.

So, to reiterate, you will use a 1D array but can use functions like: `idxToRow()`, `idxToCol()`, `getEntryAtRC()` to move back and forth between 1D and 2D, whichever is most convenient for your algorithms.

### **1D to 2D Array access**

The `grid` argument to each function is a 1D array. However, we can *visualize* it as a 2D array if we let the first `dim` elements be the first row, the next `dim` elements be the 2nd row, and so on. For a 3x3 grid, the array contents:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| X | O | ? | ? | O | X | ? | ? | X |

would correspond to a tic-tac-toe grid of:

 `X | O | ?
-----------
 ? | O | X
-----------
 ? | ? | X`

To begin, we initialize the array to contain `?` characters which would lead to the initial output:

 `? | ? | ?
-----------
 ? | ? | ?
-----------
 ? | ? | ?`

Put more concretely, below we show the **array index** correspondence to the given locations in a 3x3 grid:

 `0 | 1 | 2
-----------
 3 | 4 | 5
-----------
 6 | 7 | 8`

A 5x5 grid would have this correspondence to the 1D-array of 25 elements:

  `0 |  1 |  2 |  3 |  4
------------------------
  5 |  6 |  7 |  8 |  9
------------------------
 10 | 11 | 12 | 13 | 14
------------------------
 15 | 16 | 17 | 18 | 19
------------------------
 20 | 21 | 22 | 23 | 24`

We assume the player knows this correspondence, so you need not print or show such a grid (i.e. one with location numbers) to the user. You will print the actual game board with `X`, `O`, and `?` characters.

### **Using math to determine row and column indexing**

1. Consider the problem of iterating through row 0 of the grid. (Let us assume we count rows and columns starting at 0 like an array not 1).

For a 3x3 grid:

- the 0th row starts at `grid[0]`
- the 1st row starts at `grid[3]`
- the 2nd row starts at `grid[6]`

For a 5x5 grid:

- the 0th row starts at `grid[0]`
- the 1st row starts at `grid[5]`
- the 2nd row starts at `grid[10]`
- the 3rd row starts at `grid[15]`
- the 4th row starts at `grid[20]`
1. Can you generalize the pattern to enumerate the array indices that form the **i-th** row? The **i-th** row starts at what index in the `grid` array? Put your answer in terms of `i` and `dim`.

Now consider the problem of iterating down a column of the grid.

- For a 3x3 grid, iterating down column 0 would mean visiting indices: `0`, `3`, `6`
- For a 3x3 grid, iterating down column 1 would mean visiting indices: `1`, `4`, `7`
- For a 3x3 grid, iterating down column 2 would mean visiting indices: `2`, `5`, `8`
- For a 5x5 grid, iterating down column 0 would mean visiting indices: `0`, `5`, `10`, `15`, `20`
- For a 5x5 grid, iterating down column 1 would mean visiting indices: `1`, `6`, `11`, `16`, `21`
- For a 5x5 grid, iterating down column 2 would mean visiting indices: `2`, `7`, `12`, `17`, `22`
- and so on…

Can you generalize the pattern? To iterate down column **i**, we should start at what index in the array? Then we should take steps of what size? Put your answer in terms of `i` and `dim`.

1. Finally, consider how, if you had a given row and column location (i.e. **row** and **col**) you might determine what index in the 1D-array corresponds to that location.
- For a 3x3 grid, row=`0`, col=`1` corresponds to index `1`
- For a 3x3 grid, row=`1`, col=`0` corresponds to index `3`
- For a 3x3 grid, row=`1`, col=`1` corresponds to index `4`
- For a 3x3 grid, row=`1`, col=`2` corresponds to index `5`
- For a 3x3 grid, row=`2`, col=`0` corresponds to index `6`
- For a 3x3 grid, row=`2`, col=`1` corresponds to index `7`
- For a 3x3 grid, row=`2`, col=`2` corresponds to index `8`
- For a 5x5 grid, row=`0`, col=`1` corresponds to index `1`
- For a 5x5 grid, row=`1`, col=`0` corresponds to index `5`
- For a 5x5 grid, row=`1`, col=`1` corresponds to index `6`
- For a 5x5 grid, row=`1`, col=`2` corresponds to index `7`
- For a 5x5 grid, row=`1`, col=`3` corresponds to index `8`
- For a 5x5 grid, row=`1`, col=`4` corresponds to index `9`
- For a 5x5 grid, row=`4`, col=`0` corresponds to index `20`
- For a 5x5 grid, row=`4`, col=`1` corresponds to index `21`
- For a 5x5 grid, row=`4`, col=`2` corresponds to index `22`
- For a 5x5 grid, row=`4`, col=`3` corresponds to index `23`
- For a 5x5 grid, row=`4`, col=`4` corresponds to index `24`

Can you generalize the pattern? Given `row` and `col` numbers could you find a mathematical expression to convert to the 1D index of the square that corresponds to that row and column? Note that this relationship should help you visit the diagonals because it might be easier to consider generating two separate indices: `row` and `col` and then converting those two values to the corresponding 1D array index.

1. To summarize you should be able to complete the following conversions using simple mathematical expressions:
- Given a 1D array index, call it `i`, (e.g. for a 5x5 grid suppose you are given an index between 0-24), the row and column corresponding to that location, `i`, can be found as:
    - **`row = __________________ (in terms of i and dim)`**
    - **`col = __________________ (in terms of i and dim)`**

Use the answers you found above to complete the functions `idxToRow(int i, int dim);` and `idxToCol(int i, int dim);`. With those functions, you can call them anywhere in your code that you may want to conver a 1D index to a 2D row/column index, if it is helpful.

- Given a `row` and `column` index and the dimension of the board `dim` we can convert to the 1D array index, call it `i`, by performing:
    - **`i = ____________________ (in terms of row, col, and dim)`**

Use the answer you just found to complete the function `getEntryAtRC(char grid[], int dim, int r, int c);`. Call this function anywhere you might find it convenient to generate two separate indices (row, column) and then to access the corresponding character (`X`, `O`, etc.) from the grid at that row/column index.

### **Output**

Your grid must be drawn in a **2D** format according to the examples shown below. Consider which visualization and indexing (1D or 2D) will be most natural to this task, write loops to generate those indices, and then, if necessary, use the conversion functions described above (e.g. `getEntryAtRC()`) to access the array elements.

- Sample 3x3 Grid Output format:

 `X | O | ?
-----------
 ? | O | X
-----------
 ? | ? | X`

- Sample 5x5 Grid Output format:

 `X | O | ? | ? | ?
-------------------
 ? | O | X | X | ?
-------------------
 ? | ? | X | O | ?
-------------------
 ? | X | O | O | ?
-------------------
 ? | ? | X | O | ?`

Notice there is a space **before** and **after** each `X`, `O`, and `?`. And, if it is not clear, there are NO blank rows. The first row is immediately followed by a row of dashes (e.g. `------`), then the second row of X, O, ?, followed by another row of dashes, and so on.

### **Getting Input**

**The first play of the game should be made by player `X`.** Then, at each turn you should prompt the user to enter the square number that they want to choose for their location. A simple prompt such as the one shown below would suffice, but should at least show whose turn it is (Player `X` or `O`) and the legal input range: 00 to dim2−1dim2−1.

*`"Player X enter your square choice [0-8]: "`*

**Important Requirements**:

- If the user enters an integer that lies outside the range  to , then your program should quit without printing other status messages .
  
    0
    
    0
    
    dim2−1
    
    dim2−1
    
- If the user chooses a square that is **already occupied** with an `X` or `O`, then prompt the user to choose again (using the same prompt format shown above) **and continue doing so until they choose a blank square or give an out-of-bounds location**.

Once an open, valid location is chosen, update the `tttdata` array. We have then provided code in `main()` to print out the updated board using `printTTT()`.

**Important**: We have already inserted the call to `printTTT()` in `main()` in between where we ask you to write the code to get the user input and where we ask you to write code to check the game status. So, unless the user entered a location outside the legal range and you exit the program, the board should be printed (via our call to `printTTT()`) after getting an input.

Consider how some or all of this task of receiving input can be extracted into a function that is called by `main()`. Feel free to organize your code as such.

### **Hints**

- **Be sure to indent your code correctly and add comments describing major chunks of your code. See the visual rubric on the last page.**
- For the `void printTTT(char grid[], int dim)` it will likely be useful to use nested loops (one loop generating a row index and the other a column index). Remember, if you correctly completed the `getEntryAtRC(char grid[], int dim, int r, int c)` function described above, you can use your row, column indices to get the corresponding character from the grid array. Take care of spacing and printing the `|` and `` (vertical and horizontal separators).
  
    You must match the spacing format shown in this document.
    
- For `int checkForWinner(char grid[], int dim);` there are several possible approaches but the easiest is likely to write one set of loops to walk down each row and see if all the locations have the same `X` or `O` character. Again, nested for loops can help generate the row, column indices and the `getEntryAtRC` function can retrieve the corresponding character. Only then would you need to walk down each of the columns to see if any column has all the same player letters. Finally, you can use one loop to walk each diagonal (first the top-left to bottom-right diagonal, followed by the top-right to bottom-left diagonal). Don’t try to check everything at once but break the code into portions: first check rows, then columns, then diagonal 1, then diagonal 2. In some ways this is similar to the **[Distributed-OR (Succeed Early / Fail Late) Idiom](https://bytes.usc.edu/cs103/idioms.html#distributed-or)** in that if you find just one row, column OR diagonal with all Xs or all Os, we have a winner and can return our answer.
- For `bool checkForDraw(char grid[], int dim)` you should likely use a similar strategy as `checkForWinner`. Remember, to be a draw each row, each column, and each diagonal must have 1 of each player letter: `X` and `O`. IN some ways this is similar to the **[Distributed-AND (Fail Early / Succeed Late) Idiom](https://bytes.usc.edu/cs103/idioms.html#distributed-and)** in that we have to prove ALL rows, columns and diagonals have at least 1 `X` and 1 `O`. If we find any row that doesn’t have any Os or any Xs we can stop early and it is NOT a draw yet. So you can iterate down each row looking for a row that proves it is not a draw. Then you can iterate down each column looking for a column that proves it is not a draw. Finally, you can iterate down the two diagonals separately.

### **Build and Run**

Since we have taught you to compile your code using `g++` and run your code on the command line, you will need to compile and test your code on your own in the Terminal window/area at the bottom of the Codio window. Review Lab 1 and/or lecture slides if you’ve forgotten. **The executable program must be named `tttn`**.

### **Testing Your code**

You should run your program in the terminal area a few times and play the game to ensure things work as expected.

### **Grading Your code**

The next page contains various tests that will exercise your code. Passing those tests is how you will earn the score on your exam. Be sure you run all the checks.
