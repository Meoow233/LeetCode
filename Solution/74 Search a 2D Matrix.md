# 74 Search a 2D Matrix

Write an efficient algorithm that searches for a value in an *m* x *n* matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

**Example 1:**

```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
```

**Example 2:**

```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false
```



#### First try   			**O(m + n)**

same as 240

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length <= 0 || matrix[0].length <= 0)
            return false;
        int row = 0;
        int col = matrix[0].length -1;
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
}
```

**O(m + n)**



#### Second try -- from bottom left

```java
class Solution {
	public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length <= 0 || matrix[0].length <= 0)
            return false;
        int row = matrix.length-1;
        int col = 0;
        while (row >= 0 && col <= matrix[0].length-1) {
            if (matrix[row][col] == target)
                return true;
            else if (matrix[row][col] > target)
                row--;
            else
                col++;
        }
        return false;  
    }
}
```



#### Third try -- treated as a sorted list and use binary search 	O(log m + log n)

```java
n * m matrix convert to an array => matrixx => a[x * m + y]
an array convert to n * m matrix => a[x] =>matrixx / m
```



```java
class Solution {
	public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length <= 0 || matrix[0].length <= 0)
            return false;
        int row = matrix.length, col = matrix[0].length;
        int start = 0, end = row * col - 1;
        while (start <= end) {
            int mid = (start + end) / 2;
            if (matrix[mid/col][mid%col] == target)
                return true;
            else if (matrix[mid/col][mid%col] < target)
                start = mid + 1;
            else
                end = mid - 1;
        }
        return false;            
    }
}
```



