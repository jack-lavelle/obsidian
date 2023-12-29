### Easy Problems

#### Invert Binary Tree

Tree problems are somewhat tricky in that there can, sometimes, be various applicable algorithms and, as such, every problem can have multiple solutions.

##### Recursive Solution
This is a somewhat easy problem (though I could not remember the solution when I first returned to it $\rightarrow$ I do not understand it as much as I *should*.)

- [ ] #leetcode #trees #first-warning This will be marked as completed when I have proven that I can return to tree problems and solve them.

```python
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
	    # Recursion requires a base case and this is it.
        if not root:
            return
		
		# Preserve `root.left` since it will be needed when re-assigning `root.right` 
        original_left = root.left
        root.left = self.invertTree(root.right)
        root.right = self.invertTree(original_left)

        return root
```

###### This solution is *not* scalable!

This solution does not scale for "deep" trees since [[Areas to Research#Stack Overflows in Response to Recursion|it would add too many recursive calls to the stack frame, potentially causing a stack overflow]].

#### Maximum Depth of Binary Tree
Three kinds of solutions for this: DFS, BFS, and recursive solutions.

Here is the (self-invented) recursive:
```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return max(self.maxDepth(root.left) + 1, self.maxDepth(root.right) + 1)
```