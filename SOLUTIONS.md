# Nested Loops and 2D Arrays — Annotated Solutions

---

## Problem 1 — Repeat Each Value Three Times

**Strategy:** Use the outer loop to visit each element of the array, and use the inner loop as a fixed counter that runs exactly 3 times — independent of the array's contents. The inner loop's job is repetition, not scanning.

Notice that the inner loop's condition (`times < 3`) has nothing to do with the array — it's just a counter. This is a useful pattern whenever you want to repeat an action a fixed number of times for each element.

```java
public void run() {
    int[] nums = {4, 2, 9};

    for (int i = 0; i < nums.length; i++) {
        System.out.print("Index " + i + ": ");

        // Inner loop runs exactly 3 times per element, not once per array slot
        for (int times = 0; times < 3; times++) {
            System.out.print(nums[i] + " ");
        }

        System.out.println(); // Move to the next line after each element's three prints
    }
}
```

---

## Problem 2 — Print All Ordered Pairs

**Strategy:** Both loops iterate over the full array, producing every possible `(i, j)` combination — including pairs where `i == j`. This prints `n²` pairs total. The word "ordered" means `(3, 6)` and `(6, 3)` are considered different pairs, so we don't skip any combinations.

Contrast this with Problem 5, where we use `j = i + 1` to avoid counting the same pair twice. Here, order matters, so all combinations are printed.

```java
public void run() {
    int[] nums = {3, 6};

    // Both loops cover the full array — no restrictions on i or j
    for (int i = 0; i < nums.length; i++) {
        for (int j = 0; j < nums.length; j++) {
            System.out.println("(" + nums[i] + ", " + nums[j] + ")");
        }
    }
}
```

---

## Problem 3 — Count Later Occurrences of First Element

**Strategy:** This problem only needs a single loop — no nesting required. Save the target value at index 0, then scan the rest of the array starting at index 1. Starting the loop at `i = 1` is the key: it means we're checking every element *after* the first, which is exactly what "later occurrences" means.

```java
public void run() {
    int[] nums = {7, 1, 7, 3, 7};

    int target = nums[0]; // Save the value at index 0 before the loop
    int count = 0;

    // Start at index 1 to look only at elements after the first
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] == target) {
            count++;
        }
    }

    System.out.println(count);
}
```

---

## Problem 4 — Print All Increasing Pairs

**Strategy:** Use nested loops to compare every possible pair `(i, j)` and print the pair only when `nums[j] > nums[i]`. Since order matters here — `(2, 8)` is a valid increasing pair but `(8, 2)` is not — both loops cover the full array, and the condition handles the filtering.

Notice that pairs where `i == j` are automatically excluded by the condition (`nums[i]` is never greater than itself). No special handling for that case is needed.

```java
public void run() {
    int[] nums = {8, 5, 2};

    for (int i = 0; i < nums.length; i++) {
        for (int j = 0; j < nums.length; j++) {

            // Only print when j's value is strictly greater than i's value
            if (nums[j] > nums[i]) {
                System.out.println("(" + nums[i] + ", " + nums[j] + ")");
            }
        }
    }
}
```

---

## Problem 5 — Count Pairs Differing by Exactly 1

**Strategy:** Use `j = i + 1` in the inner loop so that each pair is only examined once. Without this, the pair at indexes `(0, 1)` and `(1, 0)` would both be counted, doubling the result. Starting `j` after `i` also prevents comparing an element to itself.

`Math.abs()` computes the absolute value of the difference, so the check works regardless of which value is larger.

```java
public void run() {
    int[] nums = {4, 5, 7, 8};

    int count = 0;

    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) { // j starts after i to avoid duplicate pairs

            // Math.abs handles both (5-4) and (4-5) correctly
            if (Math.abs(nums[i] - nums[j]) == 1) {
                count++;
            }
        }
    }

    System.out.println("Pairs differing by 1: " + count);
}
```

---

## Problem 6 — Print 2D Array Dimensions

**Strategy:** Access `grid.length` for the total number of rows. Then loop through each row and access `grid[r].length` for the column count of that specific row. This works correctly even for jagged arrays (rows of unequal length), like the one used here.

This problem demonstrates why you should always use `grid[r].length` — not `grid[0].length` — in the inner loop when rows may differ in size.

```java
public void run() {
    int[][] grid = {
        {2, 4},
        {6, 8, 10},
        {5}
    };

    System.out.println("Row count: " + grid.length); // grid.length = number of rows

    // Each row is its own array — grid[r].length gives its individual column count
    for (int r = 0; r < grid.length; r++) {
        System.out.println("Row " + r + " has " + grid[r].length + " columns");
    }
}
```

---

## Problem 7 — Print the Grid in Row-Major Order

**Strategy:** Row-major traversal is the standard way to visit every cell in a 2D array. The outer loop moves through rows, and the inner loop moves through each column within that row. `System.out.print` keeps values on the same line; `System.out.println()` ends the row.

```java
public void run() {
    int[][] grid = {
        {1, 2, 3},
        {4, 5, 6}
    };

    for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[r].length; c++) {
            System.out.print(grid[r][c] + " "); // Stay on the same line within a row
        }
        System.out.println(); // End the current row before starting the next
    }
}
```

---

## Problem 8 — Compute the Sum of Each Row

**Strategy:** Declare the `sum` variable *inside* the outer loop so it resets to zero for each new row. If `sum` were declared outside, it would accumulate across all rows, giving you the grand total instead of per-row sums.

This is a common pattern: declare accumulators at the level where they need to reset.

```java
public void run() {
    int[][] grid = {
        {3, 1},
        {2, 9}
    };

    for (int r = 0; r < grid.length; r++) {
        int sum = 0; // Reset to 0 at the start of each row

        for (int c = 0; c < grid[r].length; c++) {
            sum += grid[r][c];
        }

        System.out.println("Row " + r + " sum: " + sum);
    }
}
```

---

## Problem 9 — Compute Column Sums

**Strategy:** Swap the loop order to use column-major traversal: the outer loop selects a column, and the inner loop walks down all rows in that column. This is the opposite of row-major order.

Because column-major traversal assumes all rows share the same number of columns, this solution stores `grid[0].length` as `cols` upfront. (If the array were jagged, you'd need a different approach.)

```java
public void run() {
    int[][] grid = {
        {2, 3, 4},
        {5, 6, 7}
    };

    int rows = grid.length;
    int cols = grid[0].length; // Safe here because all rows have the same length

    // Outer loop picks the column; inner loop walks down all rows in that column
    for (int c = 0; c < cols; c++) {
        int sum = 0;

        for (int r = 0; r < rows; r++) {
            sum += grid[r][c]; // grid[r][c] — row varies, column stays fixed
        }

        System.out.println("Column " + c + " sum: " + sum);
    }
}
```

---

## Problem 10 — Count Values Greater Than 10

**Strategy:** Standard row-major traversal with a counter. The counter is declared outside both loops so it accumulates across the entire grid — unlike Problem 8 where it reset per row. Choosing where to declare the accumulator determines its scope.

```java
public void run() {
    int[][] grid = {
        {4, 11, 9},
        {15, 2, 7}
    };

    int count = 0; // Declared outside both loops to persist across the entire grid

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

---

## Problem 11 — Find the Largest Value

**Strategy:** Initialize `max` to `grid[0][0]` — the very first element — rather than to `0`. If all values in the grid were negative, starting at `0` would produce an incorrect result since no value would ever exceed it. Starting at an actual element from the grid guarantees the initial value is valid.

Then scan every cell, updating `max` whenever a larger value is found.

```java
public void run() {
    int[][] grid = {
        {4, 8, 1},
        {3, 18, 6},
        {7, 2, 5}
    };

    int max = grid[0][0]; // Start with a real value, not an assumption like 0

    for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[r].length; c++) {

            if (grid[r][c] > max) {
                max = grid[r][c]; // Update whenever we find a new largest value
            }
        }
    }

    System.out.println("Max value: " + max);
}
```

---

## Problem 12 — Count Even Numbers in Each Row

**Strategy:** Declare `count` inside the outer loop so it resets to zero at the start of each row. This is the same scoping pattern from Problem 8 — the placement of the declaration controls whether the variable persists across rows or resets.

The even check uses the modulus operator: `value % 2 == 0` is true when a number divides evenly by 2.

```java
public void run() {
    int[][] grid = {
        {2, 5, 9},
        {4, 6, 8},
        {1, 3, 7}
    };

    for (int r = 0; r < grid.length; r++) {
        int count = 0; // Resets for each row

        for (int c = 0; c < grid[r].length; c++) {

            if (grid[r][c] % 2 == 0) { // % 2 == 0 means even
                count++;
            }
        }

        System.out.println("Row " + r + " evens: " + count);
    }
}
```

---

## Problem 13 — Identify Strictly Increasing Rows

**Strategy:** Use a boolean flag `increasing`, initialized to `true`. The inner loop compares each adjacent pair of values; if any pair violates the "strictly increasing" rule, the flag is set to `false` and `break` exits the inner loop early — there's no point checking further once we know the row fails.

Two key details:
- The inner loop ends at `grid[r].length - 1` (not `grid[r].length`) because we look ahead to `c + 1`. Going to the last index would cause an out-of-bounds error.
- `>=` in the condition catches both equal values and decreasing values, since "strictly increasing" requires each next value to be *greater than* (not equal to) the previous.

```java
public void run() {
    int[][] grid = {
        {2, 5, 9},
        {3, 3, 8},
        {1, 4, 7}
    };

    for (int r = 0; r < grid.length; r++) {
        boolean increasing = true; // Assume the row is increasing until proven otherwise

        // Stop one before the last element since we look ahead to c+1
        for (int c = 0; c < grid[r].length - 1; c++) {

            if (grid[r][c] >= grid[r][c + 1]) { // Equal counts as NOT strictly increasing
                increasing = false;
                break; // No need to check the rest of this row
            }
        }

        if (increasing) {
            System.out.println("Row " + r + " is strictly increasing");
        }
    }
}
```

---

## Problem 14 — Count Values Matching Their Row Index

**Strategy:** The row index `r` is already available as the outer loop variable. Inside the inner loop, simply compare each cell's value to `r`. This is a good example of using loop variables for something beyond just bounds-checking.

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

            if (grid[r][c] == r) { // Compare the cell's value to its row index
                matches++;
            }
        }
    }

    System.out.println("Matches row index: " + matches);
}
```

---

## Problem 15 — Find the First Occurrence of a Target

**Strategy:** Use a boolean flag `found` to break out of both loops once the target is located. A single `break` only exits the innermost loop — to stop the outer loop too, check the flag at the top of the outer loop and `break` again.

This two-level break pattern is the standard way to do an early exit from nested loops in Java. (An alternative is to put the logic in a method and use `return`, but the flag approach works well here.)

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
                break; // Exit the inner loop
            }
        }
        if (found) break; // Exit the outer loop too
    }

    if (!found) {
        System.out.println("Not found");
    }
}
```
