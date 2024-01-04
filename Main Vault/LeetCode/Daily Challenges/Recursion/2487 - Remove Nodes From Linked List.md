## Timeline

You are given a linked list and any node where a larger number is to the right of said node must be removed.
## The Recursive Solution

### High Level Understanding

This recursive solution works from the right side of the list to the list by recursively assigning the `node.next` value to the recursive function call. Each return of the recursive function call builds the list that is to be returned.

The recursion works as follows:
1) If there is no `node` then return `None`,
2) We reverse the list AND remove the elements as needed;
	i - list reversion is done by assigning `node.next` to the return value of the method itself with the argument of `node.next`.
	ii - the appropriate elements are implicitly removed when `node.next > node` by returning `node.next` rather than the `node`. 
### Code
#### Implementation
```Python
class Solution:
    def removeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head: return None
        head.next = self.removeNodes(head.next)
        if head.next and head.next.val > head.val:
            return head.next
        return head
```
## Solution 2

- [ ] #1/4/2024 Complete another solution (iteratively or using a stack maybe)
### High Level Understanding.

My high level explanation.
#### Code
##### Preliminary and Original Implementation (if I can think of something on my own)
```Python
my terrible solution
```
##### Borrowed Implementation
```Python
This is usually another answer than mine.
```
##### Improved 
```Python
This is the combination of my own thoughts and the solution I found.
```