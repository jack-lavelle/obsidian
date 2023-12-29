## Easy Problems
### Valid Parentheses

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
