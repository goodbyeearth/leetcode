# [200. 岛屿数量] (https://leetcode-cn.com/problems/number-of-islands/)

# 方法1
利用一个表记录访问过的位置，DFS.
```
class Solution:        
    def numIslands(self, grid: List[List[str]]) -> int:
        def broadcast(grid, i, j):
            self.visited_map[i][j] = 1
            if i>0 and self.visited_map[i-1][j]==0 and grid[i-1][j]=='1':
                broadcast(grid, i-1, j)
            if i<self.row-1 and self.visited_map[i+1][j]==0 and grid[i+1][j]=='1':
                broadcast(grid, i+1, j)
            if j>0 and self.visited_map[i][j-1]==0 and grid[i][j-1]=='1':
                broadcast(grid, i, j-1)
            if j<self.col-1 and self.visited_map[i][j+1]==0 and grid[i][j+1]=='1':
                broadcast(grid, i, j+1)
                
        res = 0
        self.row = len(grid)
        if self.row==0:
            return res
        self.col = len(grid[0])
        
        self.visited_map = [[0]*self.col for _ in range(self.row)]
        
        for r in range(self.row):
            for c in range(self.col):
                if self.visited_map[r][c]==0 and grid[r][c]=='1':
                    broadcast(grid, r, c)
                    res += 1
        
        return res
```

# 方法2
并查集
```
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        
        class UnionFind:
            def __init__(self, n):
                self.count = n
                self.parent = [i for i in range(n)]
                self.rank = [1 for _ in range(n)]
                
            def get_count(self):
                return self.count
            
            def find(self, x):
                if self.parent[x] != x:
                    self.parent[x] = self.find(self.parent[x])   # 递归寻父，同时修改 parent 指针指向根节点。
                    return    self.parent[x]
                return x     # 只有根节点才返回本身
            
            def union(self, x, y):
                x_root = self.find(x)
                y_root = self.find(y)
                
                if x_root == y_root:   # 在同一集合，什么都不操作
                    return
                
                # 树深较小的集合并入另一集合
                if self.rank[x_root] < self.rank[y_root]:    
                    self.parent[x_root] = y_root
                elif self.rank[x_root] > self.rank[y_root]:
                    self.parent[y_root] = x_root
                # 树深一致，则随意并入，并且被合并的一方树深加 1
                else:
                    self.parent[y_root] = x_root
                    self.rank[x_root] += 1
                
                self.count = self.count - 1    # 合并完集合数量减1
        
        row = len(grid)
        if row==0:
            return 0
        col = len(grid[0])
        
        uf = UnionFind(row*col)
        water_idx = None
        
        for i in range(row):
            for j in range(col):
                idx = i*col + j
                if grid[i][j]=='0':
                    if water_idx is None:
                        water_idx = idx
                    uf.union(water_idx, idx)
                else:
                    if j<col-1 and grid[i][j+1]=='1':   # 当前节点的右邻域
                        uf.union(idx, idx+1)
                    if i<row-1 and grid[i+1][j]=='1':   # 当前节点的下邻域
                        uf.union(idx, idx+col)

        return uf.get_count() if water_idx is None else uf.get_count() - 1    # 若有水域的话需要减掉水域所在的集合个数 1
```