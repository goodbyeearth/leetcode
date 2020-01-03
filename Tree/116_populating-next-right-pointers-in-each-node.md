# [116. 填充每个节点的下一个右侧节点指针] (https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)

# 方法1
在当前层节点的next都被标记好的情况下，就可以进行常数级空间的遍历了，此时对下一层所有节点的 next 进行标记。


```
class Solution(object):
    def connect(self, root):
        if root is None:
            return root
        root.next = None
        level_head = root   # 每一层最左边的结点
        p = level_head
        
        while level_head.left is not None:
            p.left.next = p.right
            if p.next is None:
                p.right.next = None
                p = level_head.left
                level_head = level_head.left
            else:
                p.right.next = p.next.left
                p = p.next
        return root
```