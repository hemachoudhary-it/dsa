```java
import java.util.Arrays;

public class Solution {

    // Approach 1: Sorting-based solution (Time: O(n log n))
    public int getSecondLargestBySorting(int[] nums) {
        if (nums.length < 2) return -1;

        Arrays.sort(nums); // Sort in ascending order
        int largest = nums[nums.length - 1];

        // Traverse from second last element to find the next smaller unique element
        for (int i = nums.length - 2; i >= 0; i--) {
            if (nums[i] < largest)
                return nums[i];
        }

        return -1; // All elements are the same
    }

    // Approach 2: Two-pass linear scan (Time: O(n))
    public int getSecondLargestTwoPass(int[] nums) {
        if (nums.length < 2) return -1;

        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        // First pass: find the largest number
        for (int num : nums) {
            if (num > largest)
                largest = num;
        }

        // Second pass: find the second largest less than the largest
        for (int num : nums) {
            if (num != largest && num > secondLargest)
                secondLargest = num;
        }

        return (secondLargest == Integer.MIN_VALUE) ? -1 : secondLargest;
    }

    // Approach 3: Optimal one-pass approach (Time: O(n))
    public int getSecondLargestOnePass(int[] nums) {
        if (nums.length < 2) return -1;

        int largest = nums[0];
        int secondLargest = Integer.MIN_VALUE;

        for (int num : nums) {
            if (num > largest) {
                secondLargest = largest;
                largest = num;
            } else if (num < largest && num > secondLargest) {
                secondLargest = num;
            }
        }

        return (secondLargest == Integer.MIN_VALUE) ? -1 : secondLargest;
    }

    // Test all approaches
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[][] testCases = {
            {10, 20, 5},
            {10, 10, 10},
            {5, 7, 3, 9},
            {1},
            {-1, -3, -2}
        };

        for (int[] test : testCases) {
            System.out.println("Array: " + Arrays.toString(test));
            System.out.println("Sorting-based: " + sol.getSecondLargestBySorting(test.clone()));
            System.out.println("Two-pass:      " + sol.getSecondLargestTwoPass(test.clone()));
            System.out.println("One-pass:      " + sol.getSecondLargestOnePass(test.clone()));
            System.out.println("-------------------------------------------------");
        }
    }
}
```

---

### 🧪 Sample Output:

```
Array: [10, 20, 5]
Sorting-based: 10
Two-pass:      10
One-pass:      10
-------------------------------------------------
Array: [10, 10, 10]
Sorting-based: -1
Two-pass:      -1
One-pass:      -1
-------------------------------------------------
Array: [5, 7, 3, 9]
Sorting-based: 7
Two-pass:      7
One-pass:      7
-------------------------------------------------
Array: [1]
Sorting-based: -1
Two-pass:      -1
One-pass:      -1
-------------------------------------------------
Array: [-1, -3, -2]
Sorting-based: -2
Two-pass:      -2
One-pass:      -2
-------------------------------------------------
```
