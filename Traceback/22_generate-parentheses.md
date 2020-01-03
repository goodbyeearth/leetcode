# [22. 括号生成] (https://leetcode-cn.com/problems/generate-parentheses/)

# 方法1 
只要左括号数量不超过n，就可以给一个左括号；只要有括号数量不超过左括号数量，就可以给个有括号。
递归递归，知道字符串长度达到2n，这个字符串必然是合法的。
```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        
        res = []
        
        # 总共2n个括号，一个个放，保证有效地放
        def traceback(S, num_left, num_right):  # 记录左右括号的数量
            if len(S)==n*2:
                res.append(S)
                return
            
            if num_left < n:
                traceback(S+'(', num_left+1, num_right)
            if num_right < num_left:
                traceback(S+')', num_left, num_right+1)
        
        traceback("", 0, 0)
        
        return res

```