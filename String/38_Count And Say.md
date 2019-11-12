# [38. Count And Say](https://leetcode-cn.com/problems/count-and-say/)
# 思路
（见代码）
```c++
class Solution {
public:
    string countAndSay(int n) {
        int p;
        string s="1", s_next;
        for(int i=1;i<n;i++){
            char c_pre = s[0];
            s_next = "\0";
            p=1;
            while(true){
                int count = 1;
                while(s[p]!='\0' && s[p]==c_pre){
                    p++;
                    count++;
                }
                s_next.push_back((char)(count+'0')); 
                s_next.push_back(c_pre);
                if(s[p]=='\0')
                    break;
                c_pre = s[p];
                p++;
            }
            s = s_next;
        }
        return s;
    }
};
```