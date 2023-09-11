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