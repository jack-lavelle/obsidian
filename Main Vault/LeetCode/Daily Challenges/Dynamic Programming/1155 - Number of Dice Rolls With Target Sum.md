December 26th, 2023

### The Brute Force Solution

#### High Level Understanding
#### Code
##### My Solution
```Python
class Solution:
    mod = 10 ** 9 + 7
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        if (n * k) < target:
            return 0
            
        self.dp = [[-1] * (target + 1) for _ in range(n + 1)]
        self.k = k
        return self.recursive(n, target)
        
    def recursive(self, n, target):
        if target == n == 0:
            return 1
        if target <= 0 or n == 0:
            return 0

        if self.dp[n][target] != -1:
            return self.dp[n][target]

        ways = 0
        for face_val in range(1, self.k + 1):
            ways = ways + self.recursive(n - 1, target - face_val)
        
        res = ways % self.mod
        self.dp[n][target] = res
        return res
```
### The Optimized Solution

**The Recursive Solver** - the function that does the heavy work. 
1) Set up two arrays `prev` and `curr` which will be used to iterate through the calculations, allowing for minimal memory use. Each index of the array represents a potential target sum and the value represents how many ways there are to calculate to said target sum. These arrays will change value during each simulated die roll.
2) The base case is that a target sum of 0 has only one way to be summed, and that is by rolling no die at all.
3) Now we simulate through the die rolls. Intuitively: for each die, add the value of each face to its respective index in the target sum array (`curr`). *However* this particular solution works **backwards** therefore we are calculating the `prev_sum` rather than moving forwards from the base case. Therefore, take the `current_sum` and subtract the `face_val` which we will call `prev_sum`: **IF** `prev_sum` is at least zero then there is *some* number of ways to sum to it so add that to the current value of how many ways there are to sum to `current_sum`; **ELSE** we have reached an impossible state with **ZERO** ways to be summed to (since each `face_val` is positive) **therefore** do nothing!
4) Save the result modulus `10**9 + 7`.
5) Continue that process for each possible target sum which is given by each valid combination of face values of the die and previous sums.
6) Lastly, simply return the value of `prev[target]` which represents how many ways there are to sum to `target`.

**The Driver Code** - the actual solution of this problem is simply calling the solver and passing the specific arguments given to the problem. **An important optimization is simply checking if the target sum is even possible given the number of die and the face values of said die.** 
#### Code

##### Preliminary Solution
```Python
class Solution:
    mod = 10**9 + 7
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
	    # This serves as a simple conditional check to quickly prune where it is impossible to get to target given the number of die and faces.
        if n * k < target:
            return 0
        return self.solve(n, k, target)

    def solve(self, n: int, k: int, target: int):
        # prev, curr - each index represents a sum and its value is how many ways you can sum to it.
        # We keep both of these while iterating through die rolls.
        prev = [0] * (target + 1)
        curr = [0] * (target + 1)

        # There is one way to sum to 0, and that when `n = 0`.
        prev[0] = 1

        # For as many die as we have
        for _ in range(1, n + 1):
            # For each possible sum from 1 to target
            for current_sum in range(1, target + 1):
                # Start with 0 ways to sum to said sum
                ans = 0
                # For each possible value of a die
                for face_val in range(1, k + 1):
	                # `current_sum` = `prev_sum` + `face_val`
	                # prev_sum being less than 0 is not a valid state since that is impossible, else (if it is at least 0) than there is some way to sum to it.              
	                prev_sum = current_sum - face_val
                    if prev_sum >= 0:
                        ans += prev[prev_sum]
                # Now, we have calculated all possible ways to sum to said sum with `n` die ... therefore save the result.
                curr[current_sum] = ans % self.mod
            # Lastly, the sum configuration of the next roll of the die depends on this one. Therefore, set prev to curr.
            prev = curr[:]
            
        return prev[target]
```

##### Second Solution
```Python
class Solution:
    mod = 10 ** 9 + 7
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        return 0 if (n * k) < target else self.recursive(n, k, target)
    def recursive(self, n, k, target):
        prev = [0] * (target + 1)
        curr = [0] * (target + 1)

        prev[0] = 1

        for _ in range(1, n + 1):
            # possible optimization
            for current_sum in range(1, target + 1):
                ans = 0
                for face_val in range(1, k + 1):
                    prev_sum = current_sum - face_val
                    if prev_sum >= 0:
                        ans = ans + prev[prev_sum]

                curr[current_sum] = ans % self.mod
            prev = curr[:]
        return curr[target]
```
##### Third Solution
```Python
class Solution:
    mod = 10 ** 9 + 7
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        if (n * k) < target:
            return 0
        curr = [0] * (target + 1)
        prev = [0] * (target + 1)
        prev[0] = 1

        for _ in range(1, n + 1):
            for current_sum in range(1, target + 1):
                ans = 0
                for face_val in range(1, k + 1):
                    prev_sum = current_sum - face_val
                    if prev_sum >= 0:
                        ans += prev[prev_sum]
                curr[current_sum] = ans % self.mod
            prev = curr.copy()
        return curr[target]
```