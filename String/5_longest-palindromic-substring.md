# 方法1
若s长度为n，则共有 2n-1 个中心点。
用指针p遍历s，对于单个p有两个中心点，一个是p本身，一个是p到p+1之间。
```
class Solution {
public:
    string longestPalindrome(string s) {
        string res;
        int p, left, right;
        int len, max_len=0;
        if(s.size()<=1)
            return s;
        for(p=0; p<s.size(); p++){
            /* 以p为中心点 */
            left = p-1;
            right = p+1;
            len=0;
            while(left>=0 && right<=s.size()-1 && s[left]==s[right]){
                left--;right++;
                len++;
            }
            if(len*2+1>max_len){
                max_len = len*2+1;
                res.assign(s, left+1, len*2+1);
            }
            
            /* 无中心点 */
            left = p;
            right = p+1;
            len = 0;
            while(left>=0 && right<=s.size()-1 && s[left]==s[right]){
                left--;right++;
                len++;
            }
             if(len*2>max_len){
                max_len = len*2;
                res.assign(s, left+1, len*2);
            }
        }
        return res;
    }
};
```