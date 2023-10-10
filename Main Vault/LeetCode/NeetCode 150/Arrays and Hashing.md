---

---
----

<h2 style="text-align: center;">Easy Problems</h2>

----
### Contains Duplicate

_Given an integer array `nums`, return `True` if any value appears at least twice in the array, and return `False` if every element is distinct._

#### [[Hash Table |Hash Table]]

Use a hash table to iterate through the array to keep track of elements we have already seen.  In this case, we would need to iterate through the array only once but would need to sacrifice some space complexity to get this to happen.

Ultimately both [[space and time complexity]] is $O(n)$.

##### Solution

```python
class Solution:
	def containsDuplicate(self, nums: List[int]) -> bool:
		d = {}
		for num in nums:
			if num in d:
				return True
			else:
				d[num] = True

	return False
```

#### [[Sorting |Sorting]]

You can sort the array and then check that the array is increasing, if not then you have a duplicate. This has a complexity of $O(n)$.

####

Brute Force

This solution involves checking every element against every other element and, therefore, has worst case $O(n^2)$.

---

### Valid Anagram

Given two strings `s` and `t`, return `True` if `t` is an anagram of `s`, and `False` otherwise.

#### Solution

##### Hash Table

Firstly check that the length of each `str` is the same. Then, make a hash table for each `str` where the keys are the characters and the value is their count. Then return whether the two are equal.

```python
class Solution:
	def isAnagram(self, s: str, t: str) -> bool:
		if len(s) != len(t):
			return False
		d_s, d_t = {}, {}
		for i in range(len(s)):
			d_s[s[i]] = d_s.get(s[i], 0) + 1
			d_t[t[i]] = d_t.get(t[i], 0) + 1
	return d_s == d_t
```

The time and space complexity of this is $O(n_s + n_t)$.

##### Sorting

Sort the strings then compare them. Space complexity is constant and time complexity is $O(n_s$log$n_s$ + $n_t$log$n_t)$.

---

### Two Sum

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

#### Solution

#### Hash Table

Use a hash table to store the `nums` as keys and their values as indices. This way you iterate through `nums` and, for each iteration, check if the difference between `target` and the current num is already in the hash table.

Since the conditions of the problem state that there will be a solution, no need to have an edge case for return `False` or what have you.

```python
class Solution:
	def twoSum(self, nums: List[int], target: int) -> List[int]:
		d = {}
		for i, val in enumerate(nums):
			diff = target - val
			if diff in d:
				return [i, d[diff]]

		d[val] = i
```

----
