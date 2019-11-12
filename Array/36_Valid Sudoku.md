# [36. Valid Sudoku](https://leetcode-cn.com/problems/valid-sudoku/)

# 我的思路（速度较慢）
建立一个 map, 键是数独中的数字，值是一个vector，这个vector有三个set，这三个set分别存储键这个数字在数独中的行、列、区块的编号，
逐行遍历，将每一个元素对应的行、列、区块编号存到 map 的 set 中，只要发现原来set已有某一编号就返回 false。

```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        if(board.size()==0)
            return true;
        map<char, vector<set<int>>> m;      
        set<int> r, c, b;
        vector<set<int>> v;
        int key, block;
        v.push_back(r); v.push_back(c); v.push_back(b); 
        for(int i=1; i<=9; i++){
            m.insert(pair<char, vector<set<int>>>((char)'0'+i, v));
        }
        
        for(int i=0; i<9; i++){  
            for(int j=0; j<9; j++){
                if(board[i][j]=='.')
                    continue;
                block = 3*(i/3)+j/3;
                key = board[i][j];
                r = m[key][0];
                c = m[key][1];
                b = m[key][2];
                
                if(r.find(i)!=r.end() || c.find(j)!=c.end() || b.find(block)!=b.end())
                    return false;
                r.insert(i);
                c.insert(j);
                b.insert(block);
                
                v.clear();
                v.push_back(r); v.push_back(c); v.push_back(b); 
                m[key] = v;      
            }                 
        }
        return true; 
    }
};
```

# 我的思路2（速度稍快）
```
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int table[27][9] = {0};
        for(int i=0;i<9;i++){
            for(int j=0;j<9;j++){
                if(board[i][j]=='.')
                    continue;
                int block = 3*(i/3)+j/3;
                int num = board[i][j]-'0';
                if(table[(num-1)*3][i] || table[(num-1)*3+1][j] || table[(num-1)*3+2][block])
                    return false;
                table[(num-1)*3][i] = 1;
                table[(num-1)*3+1][j] = 1;
                table[(num-1)*3+2][block] = 1;
            }
        }
        return true;
    }
};
```