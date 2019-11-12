# [14. Longest Common Prefix](https://leetcode-cn.com/problems/longest-common-prefix/)
# 思路
（见代码）
```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size()==0)
            return "";
        if(strs.size()==1)
            return strs[0];
        string s="";
        int min_len = strs[0].size();
        for(int i=1;i<strs.size();i++){
            if(min_len > strs[i].size())
                min_len = strs[i].size();
        }
        for(int c=0; c<min_len; c++){
            char common_char = strs[0][c];
            bool flag = true;
            for(int i=1; i<strs.size(); i++){
                if(strs[i][c] != common_char){
                    flag = false;
                    break;
                }
            }
            if(flag)
                s.push_back(common_char);
            else
                break;
        }
        return s;
    }
};
```