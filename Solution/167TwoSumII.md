# # 167 Two sum II

Given an array of integers that is already **sorted in ascending order**, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such  that they add up to the target, where index1 must be less than index2.

**Note:**

- Your returned answers (both index1 and index2) are not zero-based.
- You may assume that each input would have *exactly* one solution and you may not use the *same* element twice.

**Example:**

```java
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```



## Thinking process

At first, use the same code for #1 intuitively, because they look pretty much the same

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < numbers.length; i++) {
            int complement = target - numbers[i];
            if(map.containsKey(complement)) {
                return new int[]{map.get(complement)+1, i+1};
            }
            map.put(numbers[i], i);
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```

Accepted, but the **runtime is comparatively slow:**

Runtime: 2 ms, faster than 28.06% of Java online submissions for Two Sum II - Input array is sorted.

Memory Usage: 37.4 MB, less than 64.48% of Java online submissions for Two Sum II - Input array is sorted.



#### Reasoning

Without HashMap, just have two pointers, A points to index 0, B points to index len - 1, shrink the scope based on the value and target comparison.

For those of you who are wondering how this works, here is a quick explanation:

 

Each sum is characterized by two indices `(i, j)`, where `0 <= i < j < n` with n the length of the input array. If we were to compute them explicitly, we end up with an `n`-by-`n` matrix.

 

If the input array is not sorted, to search for the target, there  is no good way but comparing it with elements from the above matrix one  by one. This is the naive `O(n^2)` solution. Of course you can use a HashMap to memorize visited elements and cut down the time to `O(n)` so we have the classic space-time tradeoff.

 

Now if the input array is sorted, the `n`-by-`n` summation matrix will have the following properties:

 

1. Integers in each row are sorted in ascending order from left to right.
2. Integers in each column are sorted in ascending order from top to bottom.



To find the target, we do not have to scan the whole matrix  now since it exhibits some partial order. We may start from the  top-right (or bottom-left) corner, then proceed to the next row or  previous column depending on the relationship between the matrix element  and the target until either it is found or all rows and columns are  exhausted. The key here is that we can get rid of a whole row or column  due to the two properties of the matrix specified above.



If you have finished leetcode problem ["240. Search a 2D Matrix II"](https://leetcode.com/problems/search-a-2d-matrix-ii/),  you will find that this is exactly the same problem, except now of the  two indices, the first has to be smaller than the second. Time  complexity for "leetcode 240" is `O(m + n)`, while for this problem we have `m = n`, plus the indices constraint so the time complexity will be `O(n)`. Also we do not need the HashMap now so space complexity will be `O(1)`.



```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int i = 0, j = numbers.length - 1;
        while(i < j) {
            if (numbers[i] + numbers[j] < target) i++;
            else if (numbers[i] + numbers[j] > target) j--;
            else
                return new int[]{i+1, j+1};
        }
        return new int[2];
    }
}
```







 





