# [46. 全排列] (https://leetcode-cn.com/problems/permutations/)

# 方法1
考虑将第k个元素添加到由索引 \[k+1, n\] 的元素得到的全排列：只要将第k个元素插入到某一种排列的每个位置就可以了
（假设某排列的长度为 m,需要插入的索引位置有 0,1,...,m， 共 m+1 个位置）。
```
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        # 第二位开始都已经排列完毕
        if len(nums)>1:
            ll = self.permute(nums[1:])
        elif len(nums)==1:
            return [nums]
        else:
            return res
        
        for l in ll:
            for i in range(len(l)+1):
                l2 = l[:i] + [nums[0]] + l[i:]
                res.append(l2)
        
        return res
```           
            