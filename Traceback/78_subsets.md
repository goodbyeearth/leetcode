# [78. 子集](https://leetcode-cn.com/problems/subsets/)

# 方法1
注意必须保证生成的集合不重合。helper的第一个参数是已有的一个子集，第二个参数是子集中最后的元素再往后的剩余的元素，
如nums=\[2,3,4,1\], 若 subset=\[3\], 则 rest = \[4, 1\]，不能有2出现，否则生成的子集会重合；若 subset=\[2, 4\], 则 rest=\[1\]。

```
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        res.append([])
        def helper(subset, rest):
            for i in range(len(rest)):
                t = subset+[rest[i]]
                res.append(t)
                helper(t, rest[i+1:])   # 这一句保证集合不重合
                
        helper([], nums)
        return res
```