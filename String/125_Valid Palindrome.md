# [125.Valid Palindrome](https://leetcode-cn.com/problems/valid-palindrome/)

```c++
class Solution {
public:
    bool isPalindrome(string s) {
        int i=0, j=s.size()-1;
        while(i<j){
            bool ctn = false;
            
            if(s[i]<'0' || ('9'<s[i]&&s[i]<'A') || (s[i]>'Z'&&s[i]<'a') || s[i]>'z'){
                i++;
                ctn = true;
            }
            if(s[j]<'0' || ('9'<s[j]&&s[j]<'A') || (s[j]>'Z'&&s[j]<'a') || s[j]>'z'){
                j--;
                ctn = true;
            }
            if(ctn)
                continue;
            if(('0'<=s[i] && s[i]<='9') || ('0'<=s[j] && s[j]<='9')){   
                if(s[i]!=s[j])
                    return false;
            }
            else{
                if(!(s[i]==s[j] || s[i]-s[j]=='a'-'A' || s[j]-s[i]=='a'-'A'))
                    return false;  
            }
            i++;
            j--;
        }
        return true;
    }
```