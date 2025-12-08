# Nested Loops and 2D Arrays

This lesson introduces two closely related concepts: **nested loops** and **2D arrays**. We begin by exploring how and why nested loops are used with regular 1D arrays, and then extend this understanding to 2D arrays, where nested iteration becomes a natural and essential tool.

By the end of this lesson, you will be able to:
- Understand when and why nested loops are needed
- Write nested loops that process 1D arrays
- Declare, initialize, and work with 2D arrays
- Traverse 2D arrays using nested loops
- Apply row-by-row and column-by-column processing patterns

## Part 1: Nested Loops With 1D Arrays

Recall the concept of a nested loop from the previous unit on Control Flow — a loop inside another loop. For example:

```java
for (int i = 0; i < 3; i++) {
    System.out.println("Outer loop i = " + i);

    for (int j = 0; j < 2; j++) {
        System.out.println("    Inner loop j = " + j);
    }
}
```

### When Do We Need Nested Loops?
In array handling, nested loops are useful in situations that require:
- Comparing an element to all other elements
- Checking pairs or combinations
- Running multiple passes within a single iteration

### Example: Printing All Pairs
```java
int[] nums = {4, 7, 2};

for (int i = 0; i < nums.length; i++) {
    for (int j = 0; j < nums.length; j++) {
        System.out.println(nums[i] + ", " + nums[j]);
    }
}
```

#### Output
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

### Example: Checking for Duplicates
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

#### Output
```
true
```

### Key Patterns to Notice
- The outer loop chooses a value  
- The inner loop scans the rest of the array  
- Sometimes we start the inner loop at `i + 1` to avoid repeated comparisons  

## Part 2: Introduction to 2D Arrays

### What Is a 2D Array?
A **2D array** is an array of arrays.  
You can picture it as a table, grid, or matrix.

Example:
```java
int[][] grid = {{1, 2, 3}, {4, 5, 6}};
```

Or, more clearly written:

```java
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6}
};
```

This grid has:
- 2 rows  
- 3 columns per row  

### Visualizing the Structure
It is often useful to draw out a 2D array in terms of its row and column structure:
can be pictured like this:

```
Row 0:  1  2  3
Row 1:  4  5  6
```

Or as references:

```
grid
 ├── grid[0] → {1, 2, 3}
 └── grid[1] → {4, 5, 6}
```

From these structures, we can see how:
- `grid.length` gives the number of rows  
- `grid[r].length` gives the number of columns in row `r`  

### Accessing Values
Using `[row][col]` notation with the above array:

```java
int x = grid[0][2]; // value is 3
```

### Row and Column Lengths
```java
grid.length        // number of rows
grid[0].length     // number of columns in row 0
```

## Part 3: Traversing a 2D Array With Nested Loops

### Row-Major Traversal (Most Common)

```java
for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        System.out.println("Row " + r + ", Col " + c + ": " + grid[r][c]);
    }
}
```

#### Example Output
```
Row 0, Col 0: 1
Row 0, Col 1: 2
Row 0, Col 2: 3
Row 1, Col 0: 4
Row 1, Col 1: 5
Row 1, Col 2: 6
```

### Example: Summing All Values

```java
int sum = 0;

for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        sum += grid[r][c];
    }
}
```

### Example: Counting How Many Values Are Even

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

### Column-Major Traversal (Less Common)

```java
for (int c = 0; c < grid[0].length; c++) {
    for (int r = 0; r < grid.length; r++) {
        System.out.println(grid[r][c]);
    }
}
```

## Part 4: Enhanced For Loops With 2D Arrays

```java
for (int[] row : grid) {
    for (int value : row) {
        System.out.println(value);
    }
}
```

This version is shorter and cleaner, but it does **not** give row or column indices.

## Part 5: Putting It Together

### Typical Tasks You Will Do
- Count how many times something appears in a grid  
- Find max or min values  
- Compute row or column totals  
- Search for specific values  

## Common Mistakes to Avoid
- Using `grid.length` for both loops  
- Forgetting `grid[r].length`  
- Mixing up row and column indices  

<br>

# Nested Loops and 2D Arrays — Practice Problems

Work through this set in order.  

Problems 1–5 warm up your nested-loop skills.  
Problems 6–10 introduce 2D array traversal.  
Problems 11–15 apply nested loops to real algorithmic challenges.

## Section A — Nested Loops With 1D Arrays (Warm-Up)

### 1. Repeat Each Value Three Times
Starter array:
```java
int[] nums = {4, 2, 9};
```
Task: Using nested loops, print each value three times on the same line, prefixed by its index.

Expected Output:
```
Index 0: 4 4 4
Index 1: 2 2 2
Index 2: 9 9 9
```

### 2. Print All Ordered Pairs of Values
Starter array:
```java
int[] nums = {3, 6};
```
Task: Print every ordered pair (nums[i], nums[j]).

Expected Output:
```
(3, 3)
(3, 6)
(6, 3)
(6, 6)
```

### 3. Count Later Duplicates
Starter array:
```java
int[] nums = {7, 1, 7, 3, 7};
```
Task: Count how many times a value appears again later in the array.

Expected Output:
```
2
```

### 4. Print All Increasing Pairs
Starter array:
```java
int[] nums = {8, 5, 2};
```
Task: Print all pairs (nums[i], nums[j]) where nums[j] is greater than nums[i].

Expected Output:
```
(5, 8)
(2, 8)
(2, 5)
```

### 5. Count Adjacent-Value Pairs
Starter array:
```java
int[] nums = {4, 5, 7, 8};
```
Task: Count how many pairs differ by exactly 1.

Expected Output:
```
Pairs differing by 1: 2
```

## Section B — Intro to 2D Arrays

### 6. Print the Dimensions of a 2D Array
Starter grid:
```java
int[][] grid = {
    {2, 4},
    {6, 8, 10},
    {5}
};
```
Task: Print the number of rows, then columns per row.

Expected Output:
```
Row count: 3
Row 0 has 2 columns
Row 1 has 3 columns
Row 2 has 1 column
```

### 7. Print the 2D Array as a Grid
Starter grid:
```java
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6}
};
```
Task: Use nested loops to print values row by row.

Expected Output:
```
1 2 3
4 5 6
```

### 8. Compute Row Sums
Starter grid:
```java
int[][] grid = {
    {3, 1},
    {2, 9}
};
```
Task: Print the sum of each row.

Expected Output:
```
Row 0 sum: 4
Row 1 sum: 11
```

### 9. Compute Column Sums
Starter grid:
```java
int[][] grid = {
    {2, 3, 4},
    {5, 6, 7}
};
```
Task: Print the sum of each column.

Expected Output:
```
Column 0 sum: 7
Column 1 sum: 9
Column 2 sum: 11
```

### 10. Count Values Greater Than 10
Starter grid:
```java
int[][] grid = {
    {4, 11, 9},
    {15, 2, 7}
};
```
Task: Count how many values are greater than 10.

Expected Output:
```
Values > 10: 2
```

## Section C — Applying 2D Array Algorithms

### 11. Find the Largest Value
Starter grid:
```java
int[][] grid = {
    {4, 8, 1},
    {3, 18, 6},
    {7, 2, 5}
};
```
Task: Scan the entire grid and print the largest value.

Expected Output:
```
Max value: 18
```

### 12. Count Even Numbers per Row
Starter grid:
```java
int[][] grid = {
    {2, 5, 9},
    {4, 6, 8},
    {1, 3, 7}
};
```
Task: For each row, count how many values are even.

Expected Output:
```
Row 0 evens: 1
Row 1 evens: 3
Row 2 evens: 0
```

### 13. Identify Strictly Increasing Rows
Starter grid:
```java
int[][] grid = {
    {2, 5, 9},
    {3, 3, 8},
    {1, 4, 7}
};
```
Task: Print which rows are strictly increasing.

Expected Output:
```
Row 0 is strictly increasing
Row 2 is strictly increasing
```

### 14. Count Values Matching Their Row Index
Starter grid:
```java
int[][] grid = {
    {0, 2, 0},
    {1, 1, 1},
    {3, 3, 3}
};
```
Task: Count how many values equal their row index.

Expected Output:
```
Matches row index: 2
```

### 15. Find the First Occurrence of a Target
Starter grid:
```java
int[][] grid = {
    {4, 8, 1},
    {3, 9, 6},
    {7, 2, 5}
};
```
Task: Given a target value, scan the grid. Print its location or "Not found".

Example Target: 9  
Expected Output:
```
Found at row 1, column 1
```
