# Nested Loops and 2D Arrays — Annotated Solutions

## Problem 1 — Repeat Each Value Three Times  
```java
public void run() {
    int[] nums = {4, 2, 9};

    // For each index i, print value three times
    for (int i = 0; i < nums.length; i++) {
        System.out.print("Index " + i + ": ");

        for (int times = 0; times < 3; times++) {
            System.out.print(nums[i] + " ");
        }

        System.out.println();
    }
}
```

## Problem 2 — Print All Ordered Pairs  
```java
public void run() {
    int[] nums = {3, 6};

    // Nested loops generate all ordered pairs (i, j)
    for (int i = 0; i < nums.length; i++) {
        for (int j = 0; j < nums.length; j++) {
            System.out.println("(" + nums[i] + ", " + nums[j] + ")");
        }
    }
}
```

## Problem 3 — Count Later Occurrences of First Element
```java
public void run() {
    int[] nums = {7, 1, 7, 3, 7};

    int target = nums[0];
    int count = 0;

    // Compare target only with later elements
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] == target) {
            count++;
        }
    }

    System.out.println(count);
}
```

## Problem 4 — Print All Increasing Pairs  
```java
public void run() {
    int[] nums = {8, 5, 2};

    // Compare each pair
    for (int i = 0; i < nums.length; i++) {
        for (int j = 0; j < nums.length; j++) {

            if (nums[j] > nums[i]) {
                System.out.println("(" + nums[i] + ", " + nums[j] + ")");
            }
        }
    }
}
```

## Problem 5 — Count Pairs Differing by Exactly 1  
```java
public void run() {
    int[] nums = {4, 5, 7, 8};

    int count = 0;

    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {

            if (Math.abs(nums[i] - nums[j]) == 1) {
                count++;
            }
        }
    }

    System.out.println("Pairs differing by 1: " + count);
}
```

## Problem 6 — Print 2D Array Dimensions  
```java
public void run() {
    int[][] grid = {
        {2, 4},
        {6, 8, 10},
        {5}
    };

    System.out.println("Row count: " + grid.length);

    for (int r = 0; r < grid.length; r++) {
        System.out.println("Row " + r + " has " + grid[r].length + " columns");
    }
}
```

## Problem 7 — Print the Grid in Row-Major Order  
```java
public void run() {
    int[][] grid = {
        {1, 2, 3},
        {4, 5, 6}
    };

    for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[r].length; c++) {
            System.out.print(grid[r][c] + " ");
        }
        System.out.println();
    }
}
```

## Problem 8 — Compute the Sum of Each Row  
```java
public void run() {
    int[][] grid = {
        {3, 1},
        {2, 9}
    };

    for (int r = 0; r < grid.length; r++) {
        int sum = 0;

        for (int c = 0; c < grid[r].length; c++) {
            sum += grid[r][c];
        }

        System.out.println("Row " + r + " sum: " + sum);
    }
}
```

## Problem 9 — Compute Column Sums
```java
public void run() {
    int[][] grid = {
        {2, 3, 4},
        {5, 6, 7}
    };

    int rows = grid.length;
    int cols = grid[0].length;

    for (int c = 0; c < cols; c++) {
        int sum = 0;

        for (int r = 0; r < rows; r++) {
            sum += grid[r][c];
        }

        System.out.println("Column " + c + " sum: " + sum);
    }
}
```

## Problem 10 — Count Values Greater Than 10
```java
public void run() {
    int[][] grid = {
        {4, 11, 9},
        {15, 2, 7}
    };

    int count = 0;

    for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[r].length; c++) {

            if (grid[r][c] > 10) {
                count++;
            }
        }
    }

    System.out.println("Values > 10: " + count);
}
```

## Problem 11 — Find the Largest Value  
```java
public void run() {
    int[][] grid = {
        {4, 8, 1},
        {3, 18, 6},
        {7, 2, 5}
    };

    int max = grid[0][0];

    for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[r].length; c++) {

            if (grid[r][c] > max) {
                max = grid[r][c];
            }
        }
    }

    System.out.println("Max value: " + max);
}
```

## Problem 12 — Count Even Numbers in Each Row  
```java
public void run() {
    int[][] grid = {
        {2, 5, 9},
        {4, 6, 8},
        {1, 3, 7}
    };

    for (int r = 0; r < grid.length; r++) {
        int count = 0;

        for (int c = 0; c < grid[r].length; c++) {

            if (grid[r][c] % 2 == 0) {
                count++;
            }
        }

        System.out.println("Row " + r + " evens: " + count);
    }
}
```

## Problem 13 — Identify Strictly Increasing Rows  
```java
public void run() {
    int[][] grid = {
        {2, 5, 9},
        {3, 3, 8},
        {1, 4, 7}
    };

    for (int r = 0; r < grid.length; r++) {
        boolean increasing = true;

        for (int c = 0; c < grid[r].length - 1; c++) {

            if (grid[r][c] >= grid[r][c + 1]) {
                increasing = false;
                break;
            }
        }

        if (increasing) {
            System.out.println("Row " + r + " is strictly increasing");
        }
    }
}
```

## Problem 14 — Count Values Matching Their Row Index  
```java
public void run() {
    int[][] grid = {
        {0, 2, 0},
        {1, 1, 1},
        {3, 3, 3}
    };

    int matches = 0;

    for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[r].length; c++) {

            if (grid[r][c] == r) {
                matches++;
            }
        }
    }

    System.out.println("Matches row index: " + matches);
}
```

## Problem 15 — Find the First Occurrence of a Target  
```java
public void run() {
    int[][] grid = {
        {4, 8, 1},
        {3, 9, 6},
        {7, 2, 5}
    };

    int target = 9;
    boolean found = false;

    for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[r].length; c++) {

            if (grid[r][c] == target) {
                System.out.println("Found at row " + r + ", column " + c);
                found = true;
                break;
            }
        }
        if (found) break;
    }

    if (!found) {
        System.out.println("Not found");
    }
}
```
