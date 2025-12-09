# Nested Loops and 2D Arrays

In this lesson, we'll cover:

- Why nested loops are used with 1D and 2D arrays
- How to build nested loop algorithms step-by-step
- How 2D arrays are structured internally
- How to read values, modify values, and traverse grids
- How to avoid common mistakes
- A repeatable debugging process for 2D array logic

A set of practice problems follows.


## Part 1: Nested Loops With Arrays

### What Is a Nested Loop?
Recall a nested loop is a loop written inside another loop. The inner loop completes *entirely* for every single iteration of the outer loop.

Example:
```java
for (int i = 0; i < 3; i++) {
    System.out.println("Outer loop i = " + i);

    for (int j = 0; j < 2; j++) {
        System.out.println("    Inner loop j = " + j);
    }
}
```

### Output:
```
Outer loop i = 0
    Inner loop j = 0
    Inner loop j = 1
Outer loop i = 1
    Inner loop j = 0
    Inner loop j = 1
Outer loop i = 2
    Inner loop j = 0
    Inner loop j = 1
```

Notice:
- The inner loop runs *multiple times* per outer-loop iteration.
- Nested loops allow us to compare pairs, generate combinations, or revisit the entire array repeatedly.



## Why Use Nested Loops With Arrays?

Arrays sometimes require nested loops when:
- You compare each value to every other value  
- You generate pairings  
- You run a full scan inside another scan  
- You need “all combinations” of elements  

### Example: Printing All Pairs
```java
int[] nums = {4, 7, 2};

for (int i = 0; i < nums.length; i++) {
    for (int j = 0; j < nums.length; j++) {
        System.out.println(nums[i] + ", " + nums[j]);
    }
}
```

### Output:
```
4, 4
4, 7
4, 2
7, 4
7, 7
7, 2
2, 4
2, 7
2, 2
```



## Example: Checking for Duplicates
```java
boolean hasDuplicate = false;
int[] nums = {4, 7, 2, 7};

for (int i = 0; i < nums.length; i++) {
    for (int j = i + 1; j < nums.length; j++) {
        if (nums[i] == nums[j]) {
            hasDuplicate = true;
        }
    }
}

System.out.println(hasDuplicate);
```

### Output:
```
true
```

### Why `j = i + 1`?
To avoid comparing:
- The same pair twice (e.g., comparing index 2 with index 0 after index 0 with index 2)
- An element with itself



## Key Patterns to Notice in Nested Loops
- The outer loop chooses an element.
- The inner loop processes related elements.
- Limiting the inner loop (e.g., `j = i + 1`) avoids repetition.
- Nested loops grow in runtime quickly; understanding structure is important.

<br>

## Part 2: Introduction to 2D Arrays

### What Is a 2D Array?
A 2D array is an array *of arrays*. Conceptually, you can think of it as:
- A grid  
- A table  
- A matrix  

### Example:
```java
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6}
};
```

### Visual Representation (Values)
```
Row 0:  1  2  3
Row 1:  4  5  6
```

### Visual Representation (Memory Pointers)
```
grid
 ├── grid[0] → {1, 2, 3}
 └── grid[1] → {4, 5, 6}
```

Each row is another array — a 1D array.



## Accessing Values in a 2D Array

Use:  
`grid[row][column]`

Example:
```java
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6}
};

int x = grid[0][2];  // retrieves 3
```



## Determining Dimensions

### Number of rows:
```java
grid.length
```

### Number of columns in row r:
```java
grid[r].length
```

### Important:
Rows *may not* be equal length.  
This is called a **jagged array**.

<br>

## Part 3: Traversing a 2D Array With Nested Loops

### Row-Major Order (Most Common)
This means:  
**for each row → visit each column**

```java
for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        System.out.println("Row " + r + ", Col " + c + ": " + grid[r][c]);
    }
}
```

### Sample Output:
```
Row 0, Col 0: 1
Row 0, Col 1: 2
Row 0, Col 2: 3
Row 1, Col 0: 4
Row 1, Col 1: 5
Row 1, Col 2: 6
```



### Algorithm Example: Summing All Values
This algorithm uses a row-major traversal of a 2D array along with an accumulator variable, `sum`. 

```java
int sum = 0;

for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        sum += grid[r][c];
    }
}
```


### Algorithm Example: Counting Even Numbers
This algorithm uses the same row-major traversal as above, but adds a counter variable and a modulus operation.

```java
int count = 0;

for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        if (grid[r][c] % 2 == 0) {
            count++;
        }
    }
}
```



## Column-Major Traversal
Less common but still useful. If a 2D array is laid out as a grid, column-major traversal enables totalling vertical columns, for example.

```java
for (int c = 0; c < grid[0].length; c++) {
    for (int r = 0; r < grid.length; r++) {
        System.out.println(grid[r][c]);
    }
}
```


<br>

## Part 4: Enhanced For Loops With 2D Arrays

Enhanced loops simplify syntax:

```java
for (int[] row : grid) {
    for (int value : row) {
        System.out.println(value);
    }
}
```

### Benefits:
- Cleaner and readable

### Limitations:
- Cannot access row/column index easily

<br>

## Part 5: Debugging Strategies for 2D Arrays

### Debug Tip 1 — Print Dimensions First
This confirms the `row` x `column` size of the grid with which you're working:

```java
System.out.println("Rows: " + grid.length);
System.out.println("Cols in row 0: " + grid[0].length);
```

### Debug Tip 2 — Print Coordinates
Inside loops, show the current `row` x `column` value before doing something with that data:

```java
System.out.println("Visiting (" + r + ", " + c + ")");
```

### Debug Tip 3 — Draw the Grid on Paper
Many logic errors disappear when you visualize the structure:

```
     c0   c1   c2   c3   c4
   +----+----+----+----+----+
r0 |    |    |    |    |    |
   +----+----+----+----+----+
r1 |    |    |    |    |    |
   +----+----+----+----+----+
```


### Debug Tip 4 — Use Very Small Test Grids
Example:
```
1 2
3 4
```
Small grids reveal patterns easily.


<br>

## Part 6: Common Mistakes to Avoid
- Using `grid.length` for row *and* column loops  
- Forgetting `grid[r].length` for the inner loop  
- Mixing up row and column  
- Off-by-one errors  
- Assuming every row has the same number of columns  
- Trying to access `grid[r][c]` before confirming row/column length  

<br>

# Nested Loops and 2D Arrays — Practice Problems

Work through these in order to build confidence with nested loops, 1D comparisons, and 2D traversal. The problem set is subdivided into 3 sections of 5 problems each.

Annotated solutions to these problems can be found [here](SOLUTIONS.md).

# Section A — Nested Loops With 1D Arrays (Warm-Up)

## Problem 1 — Repeat Each Value Three Times  
Starter array:
```java
int[] nums = {4, 2, 9};
```

Task:  
Use **nested loops** to print each value three times on the same line, prefixed by its index.

Expected Output:
```
Index 0: 4 4 4
Index 1: 2 2 2
Index 2: 9 9 9
```


<br>

## Problem 2 — Print All Ordered Pairs  
Starter array:
```java
int[] nums = {3, 6};
```

Task:  
Using **two nested loops**, print every ordered pair `(nums[i], nums[j])`.

Expected Output:
```
(3, 3)
(3, 6)
(6, 3)
(6, 6)
```


<br>

## Problem 3 — Count Later Occurrences of the First Element  
Starter array:
```java
int[] nums = {7, 1, 7, 3, 7};
```

Task:  
Count how many times the value at index `0` appears again later in the array.

Expected Output:
```
2
```


<br>

## Problem 4 — Print All Increasing Pairs  
Starter array:
```java
int[] nums = {8, 5, 2};
```

Task:  
Using nested loops, print all pairs `(nums[i], nums[j])` where `nums[j] > nums[i]`.

Expected Output:
```
(5, 8)
(2, 8)
(2, 5)
```

<br>


## Problem 5 — Count Pairs Differing by Exactly 1  
Starter array:
```java
int[] nums = {4, 5, 7, 8};
```

Task:  
Count how many index pairs `(i, j)` produce values whose difference is exactly 1.

Expected Output:
```
Pairs differing by 1: 2
```

<br>

# Section B — Intro to 2D Arrays

## Problem 6 — Print 2D Array Dimensions  
Starter grid:
```java
int[][] grid = {
    {2, 4},
    {6, 8, 10},
    {5}
};
```

Task:  
Print the total row count, and then print the number of columns in each row.

Expected Output:
```
Row count: 3
Row 0 has 2 columns
Row 1 has 3 columns
Row 2 has 1 column
```

<br>

## Problem 7 — Print the Grid in Row-Major Order  
Starter grid:
```java
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6}
};
```

Task:  
Use nested loops to print the grid in table form.

Expected Output:
```
1 2 3
4 5 6
```

<br>

## Problem 8 — Compute the Sum of Each Row  
Starter grid:
```java
int[][] grid = {
    {3, 1},
    {2, 9}
};
```

Task:
Compute the sum of each row and print it.

Expected Output:
```
Row 0 sum: 4
Row 1 sum: 11
```

<br>

## Problem 9 — Compute Column Sums  
Starter grid:
```java
int[][] grid = {
    {2, 3, 4},
    {5, 6, 7}
};
```

Task:  
Use **column-major traversal** to compute the sum of each column.

Expected Output:
```
Column 0 sum: 7
Column 1 sum: 9
Column 2 sum: 11
```

<br>

## Problem 10 — Count Values Greater Than 10  
Starter grid:
```java
int[][] grid = {
    {4, 11, 9},
    {15, 2, 7}
};
```

Task:  
Count all values strictly greater than 10.

Expected Output:
```
Values > 10: 2
```

<br>

# Section C — Applying 2D Array Algorithms

## Problem 11 — Find the Largest Value  
Starter grid:
```java
int[][] grid = {
    {4, 8, 1},
    {3, 18, 6},
    {7, 2, 5}
};
```

Task:  
Scan the entire grid to find the maximum value.

Expected Output:
```
Max value: 18
```


<br>

## Problem 12 — Count Even Numbers in Each Row  
Starter grid:
```java
int[][] grid = {
    {2, 5, 9},
    {4, 6, 8},
    {1, 3, 7}
};
```

Task:  
For each row, count how many values are even.

Expected Output:
```
Row 0 evens: 1
Row 1 evens: 3
Row 2 evens: 0
```

<br>

## Problem 13 — Identify Strictly Increasing Rows  
Starter grid:
```java
int[][] grid = {
    {2, 5, 9},
    {3, 3, 8},
    {1, 4, 7}
};
```

Task:  
A row is “strictly increasing” if every value is greater than the one before it.

Expected Output:
```
Row 0 is strictly increasing
Row 2 is strictly increasing
```

<br>


## Problem 14 — Count Values Matching Their Row Index  
Starter grid:
```java
int[][] grid = {
    {0, 2, 0},
    {1, 1, 1},
    {3, 3, 3}
};
```

Task:  
Count how many values equal their row index.

Expected Output:
```
Matches row index: 2
```

<br>

## Problem 15 — Find the First Occurrence of a Target  
Starter grid:
```java
int[][] grid = {
    {4, 8, 1},
    {3, 9, 6},
    {7, 2, 5}
};
```

Task:  
Given a target value, scan the grid and print the location of the **first** match.  
If the target does not appear, print “Not found.”

Example Target:
```
9
```

Expected Output:
```
Found at row 1, column 1
```
