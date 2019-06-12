# 240 Search a 2D Matrix II

Write an efficient algorithm that searches for a value in an *m* x *n* matrix. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example:**

Consider the following matrix:

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = `5`, return `true`.

Given target = `20`, return `false`.



### First try -- Brute force

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int rows = matrix.length;
        int columns = matrix[1].length;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                if (matrix[i][j] == target)
                    return true;
            }
        }
        return false;
    }
}
```

**Line 4: java.lang.ArrayIndexOutOfBoundsException: 0**

This `ArrayIndexOutOfBoundsException: 0` means that the index `0` is not a valid index for your array `args[]`, which in turn means that your array is empty.



### Second try

We start search the matrix from top right corner, initialize the current position to top right corner, if the target is greater than the value in current position, then the target can not be in entire row of current position because the row is sorted, if the target is less than the 
value in current position, then the target can not in the entire column because the column is sorted too. We can rule out one row or one column each time, so the time complexity is O(m+n).

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int rows = matrix.length;
        int columns = matrix[1].length;
        int i = 0, j = columns -1;
        if(matrix == null || rows < 1 || columns < 1)
            return false;
        while (i <= rows-1 || j >= 0) {
            if (matrix[i][j] > target) j--;
            else if (matrix[i][j] < target) i++;
            else
                return true;
        }
        return false;
    }
}
```

Runtime Error Message: 
Line 4: java.lang.ArrayIndexOutOfBoundsException: 1



```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length <= 0 || matrix[0].length <= 0)
            return false;
        int row = 0;
        int col = matrix[0].length-1;
        while (row <= matrix.length-1 && col >= 0) {
            if (matrix[row][col] == target)
                return true;
            else if (matrix[row][col] > target)
                col--;
            else
                row++;
        }
        return false;
}
```

