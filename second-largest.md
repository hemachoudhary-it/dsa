### ✅ **Approach 1: Sorting-Based Solution**
```java
import java.util.Arrays;

class Solution {
    public int getSecondLargest(int[] nums) {
        // Sort the array in ascending order
        Arrays.sort(nums);
        int length = nums.length;

        // Get the largest element (last in the sorted array)
        int largest = nums[length - 1];

        // Traverse from the second last element to the beginning
        for (int i = length - 2; i >= 0; i--) {
            // Return the first element that is less than the largest
            if (nums[i] < largest)
                return nums[i];
        }

        // If no second largest found (i.e., all elements are the same)
        return -1;
    }
}
```

#### 🔍 Time & Space Complexity:
- **Time:** O(n log n) due to sorting
- **Space:** O(1) if in-place sorting, else O(n)

---

### ✅ **Approach 2: Single-Pass, Optimal Solution**
```java
class Solution {
    public int getSecondLargest(int[] nums) {
        int length = nums.length;
        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        // First pass: Find the largest element
        for (int i = 0; i < length; i++) {
            if (nums[i] > largest)
                largest = nums[i];
        }

        // Second pass: Find the second largest (less than the largest)
        for (int i = 0; i < length; i++) {
            if (nums[i] != largest && nums[i] > secondLargest)
                secondLargest = nums[i];
        }

        // If second largest wasn't updated, return -1
        return (secondLargest == Integer.MIN_VALUE) ? -1 : secondLargest;
    }
}
```

#### 🔍 Time & Space Complexity:
- **Time:** O(n) — Two linear passes
- **Space:** O(1)

---

### 🆚 Comparison:
| Feature           | Approach 1 (Sorting) | Approach 2 (Optimal) |
|------------------|----------------------|-----------------------|
| Time Complexity   | O(n log n)           | O(n)                  |
| Space Complexity  | O(1)                 | O(1)                  |
| Stability         | Simple to write      | Slightly more complex |
| Use Case          | Small arrays, less performance sensitive | Performance-critical code |
