# Nested Loops and 2D Arrays — Full Lesson

In this lesson, you will learn:

- Why nested loops are used with 1D and 2D arrays
- How to build nested loop algorithms step-by-step
- How 2D arrays are structured internally
- How to read values, modify values, and traverse grids
- How to avoid common mistakes
- A repeatable debugging process for 2D array logic


## Part 1: Nested Loops With 1D Arrays

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



## Why Use Nested Loops With 1D Arrays?

1D arrays sometimes require nested loops when:
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

Each row is a 1D array.



## Accessing Values in a 2D Array

Use:  
`grid[row][column]`

Example:
```java
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



## Algorithm Example: Summing All Values
```java
int sum = 0;

for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        sum += grid[r][c];
    }
}
```



## Algorithm Example: Counting Even Numbers
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
Less common but useful:

```java
for (int c = 0; c < grid[0].length; c++) {
    for (int r = 0; r < grid.length; r++) {
        System.out.println(grid[r][c]);
    }
}
```



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



## Part 5: Debugging Strategies for 2D Arrays

### Debug Tip 1 — Print Dimensions First
```java
System.out.println("Rows: " + grid.length);
System.out.println("Cols in row 0: " + grid[0].length);
```

### Debug Tip 2 — Print Coordinates
Inside loops:
```java
System.out.println("Visiting (" + r + ", " + c + ")");
```

### Debug Tip 3 — Draw the Grid on Paper
Many logic errors disappear when you visualize the structure.

### Debug Tip 4 — Use Very Small Test Grids
Example:
```
1 2
3 4
```
Small grids reveal patterns easily.



## Part 6: Common Mistakes to Avoid
- Using `grid.length` for row *and* column loops  
- Forgetting `grid[r].length` for the inner loop  
- Mixing up row and column  
- Off-by-one errors  
- Assuming every row has the same number of columns  
- Trying to access `grid[r][c]` before confirming row/column length  



## Summary
You now understand:
- How nested loops work with 1D arrays  
- How 2D arrays are structured in memory  
- How to traverse grids using multiple patterns  
- How to build algorithms such as searching, counting, and summing  
- How to debug nested loop logic  
- How to avoid common pitfalls  

This foundation prepares you for the associated practice problems and all upcoming data structure work in ICS3U.

