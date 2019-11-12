# [28.Implement Strstr](https://leetcode-cn.com/problems/implement-strstr/)
# KMP

注意j是有符号数，不能直接跟needle.size()比较，否则会把-1<needle.size()判断为错，needle.size()为无符号数。
```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int i=0,j=0;
        int len1=haystack.size(), len2=needle.size();
        if(len2==0)
            return 0;
        
        int *next = getNext(needle);   

        while(i<len1 && j<len2){
            if(j==-1 || haystack[i]==needle[j]){
                i++;
                j++;
            }
            else{
                j = next[j];
            }
        }
        
        if(j==needle.size())
            return i-j;
        return -1;      
    }
	
    int* getNext(string needle){
        int len = needle.size();
        int *next = new int[len];
        next[0] = -1;
        int k = -1;
        int j = 0;
        while(j < len-1){
            if(k==-1 || needle[j]==needle[k]){
                k++;
                j++;
                next[j] = k;
            }
            else{
                k = next[k];
            }
        }
        return next;
    }
};
```