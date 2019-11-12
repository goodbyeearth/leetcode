# [48. Rotate Image](https://leetcode-cn.com/problems/rotate-image/)
# 思路
剥洋葱法：（时间复杂度O(N^2)）
一圈一圈地执行以下流程，用i作为圈数，最外围的是第一圈，总共需要执行n/2圈。
（每一圈都由4条边组成）
流程：某一圈最上面的那条边分别跟右边，下边，左边的数调换位置。
（最上面的那条边忽略最右一个点，同理，右边忽略最下边的一个点....）


```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix[0].size();
        for(int i=1; i<=n/2; i++){
            for(int j=i-1; j<=n-i-1; j++)
                swap(matrix[i-1][j], matrix[j][n-i]);
            for(int j=i-1; j<=n-i-1; j++)
                swap(matrix[i-1][j], matrix[n-i][n-j-1]);
            for(int j=i-1; j<=n-i-1; j++)
                swap(matrix[i-1][j], matrix[n-j-1][i-1]);
        }
    }
};
```

# 别人的方法
先转置矩阵，然后翻转每一行。（时间复杂度O(N^2)）
```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix[0].size();
        
        // transpose matrix
        for(int i=0; i<n; i++)
            for(int j=i+1; j<n; j++)
                swap(matrix[i][j], matrix[j][i]);
        // reverse line
        for(int i=0; i<n; i++)
            for(int j=0; j<n/2; j++)
                swap(matrix[i][j], matrix[i][n-j-1]);
    }
};
```