# [230. 二叉搜索树中第K小的元素] (https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

# 方法1
利用栈进行中序遍历

```
class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        stack = []
        p = root
        while p:
            stack.append(p)
            p = p.left
        count = 0
        while True:
            p = stack.pop()
            count += 1
            if count==k:
                return p.val
            if p.right is not None:
                p = p.right
                while p:
                    stack.append(p)
                    p = p.left
```