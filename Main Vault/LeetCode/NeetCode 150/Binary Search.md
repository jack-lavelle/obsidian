----

<h2 style="text-align: center;">Easy Problems</h2>

----
### [[Binary Search|Binary Search]]

A classic. 

*Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.*

*You must write an algorithm with `O(log n)` runtime complexity.*

Initialize pointers at start and at the end of the array. While the right does not cross over the left (they can be equal ... think of the case when `len(nums) == 1`), calculate the middle, then see how `target` relates to it. There are three cases:

1) the target is smaller than `nums[mid]`,
2) the target is larger than `nums[mid]`, and
3) the target is equal to `nums[mid]`.

The first case, adjust the right pointer to the middle element minus 1 (since we know it can't be that element). The second case, adjust the left pointer to the middle element plus 1 (for similar reasons). The third case, return `mid`.

If left *does* cross over the right then return `-1`, `target` does not exist in `nums`.

- [ ] time-complexity
#### Solution
```Python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = (left + right) // 2
            
            if target == nums[mid]:
                return mid
            elif target > nums[mid]:
                left = mid + 1
            else:
                right = mid - 1
        
        return -1
```

*Note the use of `//` for division.*
