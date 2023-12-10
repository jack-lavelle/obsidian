## Easy Problems
### Valid Parentheses

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

#### Solution

##### Stack

Two tools are required for this: 1) a [[stack|stack]], and 2) a [[hash table|hash table]] where the stack provides an easy means to store the open brackets, and the hash table makes it easy to find the corresponding closed brackets.

- [ ] time-complexity?

```Python
class Solution:
    def isValid(self, s: str) -> bool:
        brackets = {"{" : "}", "[" : "]", "(" : ")"}

        stack = []
        for b in s:
            if b in brackets:
                stack.append(b)
            elif stack:
                popped = stack.pop()
                if b != brackets[popped]:
                    return False
            else:
                return False

        return not stack
```

A different solution I came up with:
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []

        bracks = {"(" : ")", "{" : "}", "[" : "]"}
        for b in s:
            if b in bracks:
                stack.append(b)
            else:
                if not stack:
                    return False

                popped = stack.pop()
                if b != bracks[popped]:
                    return False

        return not stack
```

----
