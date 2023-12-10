### Easy Problem

### Invert Binary Tree

```python
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return
        
        original_left = root.left
        root.left = self.invertTree(root.right)
        root.right = self.invertTree(original_left)

        return root
```

### Maximum Depth of Binary Tree
Three kinds of solutions for this: DFS, BFS, and recursive solutions.

Here is the (self-invented) recursive:
```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return max(self.maxDepth(root.left) + 1, self.maxDepth(root.right) + 1)
```