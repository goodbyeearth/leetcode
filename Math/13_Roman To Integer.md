# [13. Roman To Integer](https://leetcode-cn.com/problems/roman-to-integer/)

```c++
class Solution {
public:
    int romanToInt(string s) {
        int len = s.size();
        int res = 0;
        if(len==0)
            return res;
        map<char,int> m = {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000}
        };
        
        for(int i=0;i<len;i++){
            if((s[i]=='I' || s[i]=='X' || s[i]=='C') && i+1<len){
                if(s[i]=='I' && (s[i+1]=='V'||s[i+1]=='X')){
                    res = res - m[s[i]] + m[s[i+1]];
                    i++;
                }
                else if(s[i]=='X' && (s[i+1]=='L'||s[i+1]=='C')){
                    res = res - m[s[i]] + m[s[i+1]];
                    i++;
                }
                else if(s[i]=='C' && (s[i+1]=='D'||s[i+1]=='M')){
                    res = res - m[s[i]] + m[s[i+1]];
                    i++;
                }
                else{
                    res += m[s[i]];
                }
            }
                
            else
                res += m[s[i]];
            
        }
        return res;
    }
};