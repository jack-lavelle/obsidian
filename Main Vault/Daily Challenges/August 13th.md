### ***Check If There is a Valid Partition for the Array***
___
**Summary**
This problem is a rolling [[Dynamic Programming]] problem. The prompt is as follows:

> You are given a <strong>0-indexed</strong> integer array <code>nums</code>. You >have to partition the array into one or more <strong>contiguous</strong> subarrays.
> 
> We call a partition of the array <strong>valid</strong> if each of the obtained subarrays satisfies <strong>one</strong> of the following conditions:
> 
> **1.** The subarray consists of <strong>exactly</strong> <code>2,</code> equal elements. For example, the subarray <code>[2,2]</code> is good.
> **2.** The subarray consists of <strong>exactly</strong> <code>3,</code> equal elements. For example, the subarray <code>[4,4,4]</code> is good.
> **3.** The subarray consists of <strong>exactly</strong> <code>3</code> consecutive increasing elements, that is, the difference between adjacent elements is <code>1</code>. For example, the subarray <code>[3,4,5]</code> is good, but the subarray <code>[1,3,5]</code> is not.
> 
> Return <code>true</code><em> if the array has <strong>at least</strong> one valid partition</em>. Otherwise, return <code>false</code>.

**Overview of Solution**
This problem involves iterating through the array, checking if there exists a valid partition of the array at every index `i` until either one returns `True` or, having iterated through them all, none of them do, so we return `False`.

We initialize a `dp` array, whose elements are all `-1`, to serve as a record of which indices we have proven cannot return a valid partition. We then refer to this throughout solving other indices to speed this process up, knowing that if index `i` depends on index `j`, and index `j` has already been shown to have not been able to successfully partition the array, then neither can index `i`.

The main workhorse of this problem lies in the [[recursive]] helper function `solver` which implements the checking system to go through all three conditions of a valid partition. I will leave further explanation of the solution to the comments in the code itself:

```python
class Solution:
    def validPartition(self, nums: List[int]) -> bool:
        self.nums = nums
        self.dp = [-1 for i in range(len(nums))]
        return(self.solver(0))
        
    def solver(self, i: int) -> bool:
        # arguments:
        # i - the integer representing the current index of nums that is under investigation.
        if i == len(self.nums):
            return True
        # At the beginning we set all values of the array to -1. If dp[i] does not equal -1, 
        # then we have already deduced the answer to whether if the partition was split here, would we
        # have a valid partition
        if self.dp[i] != -1:
            return self.dp[i]
        # The first condition just checks that we are not out of range.
        # The second condition is the first case of a valid partition.
        if (i + 1 < len(self.nums) and self.nums[i] == self.nums[i + 1]):
            # If we are here then the first condition _may_ be met, however, for this condition to be met
            # both the left and right side of the partition divide must hold. 
            # Therefore, we must check the right side of the partition by calling the dp solver.
            if (self.solver(i + 2)):
                # To return True here means: by partitioning on current index i on the basis that nums[i] == nums[i + 1],
                # there exists a valid partitioning of the remainder of nums.
                return True
            # Next, we check if the second condition for a valid partition can be met.
            # nums[i] == nums[i + 1] == nums[i + 2].
            if (i + 2 < len(self.nums) and self.nums[i] == self.nums[i + 2]):
                if(self.solver(i + 3)):
                    return True
        # Lastly, we check the third condition.
        if (i + 2 < len(self.nums) and self.nums[i + 1] == self.nums[i] + 1 and self.nums[i + 2] == self.nums[i] + 2):
            if (self.solver(i + 3)):
                return True
        # If none of these are True, then we know that to partition at this index i will not work.
        self.dp[i] = False
        return
```