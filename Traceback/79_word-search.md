# [79. 单词搜索] (https://leetcode-cn.com/problems/word-search/)

# 方法1 
首先要注意走过的路不能再走一遍，故要用一个表来记录是否已访问某坐标。访问某坐标后需要置为已访问，
在回溯完后应该重置为未访问。
helper 的第一个参数是一个数组表示剩余的字母列表，第一个字母应当与board的当前坐标\(i, j\)匹配，否则返回 false；
若匹配则继续递归搜索四周的节点与第二个字母及其往后是否匹配。

```
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        row = len(board)
        if row==0:
            return False
        col = len(board[0])
        
        def helper(rest_word, i, j):
            if len(rest_word) == 0:    # 匹配成功的标记
                return True                
            if i<0 or j<0 or i>=row or j>=col or board[i][j] != rest_word[0] or visited_table[i][j]==1:
                return False
            
            visited_table[i][j] = 1    # 以该坐标为出发点，置为已访问，才能继续递归往下搜索
            if helper(rest_word[1:], i-1, j) or  helper(rest_word[1:], i+1, j) or helper(rest_word[1:], i, j-1) or helper(rest_word[1:], i,  j+1):
                return True
            visited_table[i][j] = 0   # 回溯之后要把 visited_table 的当前坐标(i,j)重置为0
            return False
        
        res = False
        visited_table = [[0]*col for _ in range(row)]  # 初始化为0
        for r in range(row):
            for c in range(col):
                if board[r][c] == word[0]:
                    res = helper(word, r, c)
                    if res:
                        return True
        return False
```