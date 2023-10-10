----

<h2 style="text-align: center;">Easy Problems</h2>

----
### Valid Palindrome

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` *if it is a **palindrome**, or* `false` *otherwise*.

#### Solution

##### Two Pointers

Initialize a pointer at the end of `s` and at the beginning, then move them closer until you get a situation in which they do not match and return `False` or, if that does not happen, return `True`.

Only lower case alphanumeric characters should be considered so:

1. deal with only the lowercase string, and
2. adjust each pointer until it is on an alphanumeric character.

- [ ] time-complexity?

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = s.lower()
        l, r = 0, len(s) - 1
        while l < r:
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1
            if s[l] == s[r]:
                l += 1
                r -= 1
            else:
                return False
        return True
```

----
