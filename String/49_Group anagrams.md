# [49. Group anagrams] (https://leetcode-cn.com/problems/group-anagrams/)

# 思路
用一个 Map 来记录，键为排序好的字符串，值为排序前对应的字符串。

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        map<string, vector<string>> m;
        for(auto str:strs){
            string temp = str;
            sort(temp.begin(), temp.end());
            m[temp].push_back(str);
        }
        for(map<string, vector<string>>::iterator it=m.begin(); it!=m.end(); it++){
            res.push_back(it->second);
        }
       return res;
    }
};
```