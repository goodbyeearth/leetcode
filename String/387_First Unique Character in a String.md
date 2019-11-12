# [387.First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)
# 思路

## 思路1:
假设字符串只有26个小写字母，建立一个长为26的数组，记录每个字母出现的次数。
最后遍历字符串，返回第一个出现次数为1的字母的索引。

## C++
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        int record[26] = {0};
        int len = s.size();
        for(int i=0;i<len;i++){
            record[s[i]-'a']++;
        }
        for(int i=0;i<len;i++){
            if(record[s[i]-'a']==1)
                return i;
        }
        return -1;
    }
};
```


## 思路2
建立两个set，一个存string的所有字符，一个存重复的字符。找到第一个不再第二个set中的字符的索引。
**该方法执行时间较长。**

## C++
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        int len = s.size();
        set<char> s_set, dup_set;   
        set<char>::iterator s_it; 
        
        for(int i=0;i<len;i++){
            s_it = s_set.find(s[i]);
            if(s_it!=s_set.end()) 
                dup_set.insert(s[i]);
            else 
                s_set.insert(s[i]);
        }
        for(int i=0;i<len;i++){
            s_it = dup_set.find(s[i]);
            if(s_it==dup_set.end())
                return i;
        }
        return -1;
        
    }
};
```

