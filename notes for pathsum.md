# Recursive
Current solution
```python
        
        if not root:
            return False
        pathSum = 0
        def validPath(root: TreeNode, pathSum: int) -> bool:
            pathSum = pathSum + root.val
            if not root.left and not root.right:
                if pathSum == targetSum:
                    return True
            leftPath, rightPath = False, False
            if root.left:
                leftPath = validPath(root.left, pathSum)
            if root.right:
                rightPath = validPath(root.right, pathSum)
            return leftPath or rightPath
        return validPath(root, pathSum)
```
We can make this more optimal by making the recursive call concise. Leetcode also introduces a smarter approach that instead subtracts from the single targetSum value, rather than summing *up to* the targetSum.

```python
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        if not root.left and not root.right:
            return root.val == targetSum
        targetSum = targetSum - root.val
        return self.hasPathSum(root.left, targetSum) or self.hasPathSum(root.right, targetSum)
```
jeez bruh, I always seem to not find the optimal solution somehow.

# Iterative
for the iterative solution, we're always implementing the same solution, just with a stack that simulates the call stack.
I think the correct approach is a preorder traversal

```python
def hasPathSum(node: TreeNode, targetSum: int):
	stack = []
	if node:
		stack.append(node, node.val)
	while stack or node:
		node, val = stack.pop()
		if not node.left and not node.right:
			if val == targetSum:
				return True
		if node.left:
			stack.append(node.left, node.left.val + val)
		if node.right:
			stack.append(node.right, noe.right.val + val)
		
	return False
		
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ2NDU5NzQ3XX0=
-->