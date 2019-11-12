# [242.Valid Anagram](https://leetcode-cn.com/problems/valid-anagram/)

# 思路
用大小为26的数组存储各个字母出现的次数。
```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int len_s = s.size(), len_t = t.size();
        if(len_s != len_t)
            return false;
        int record_s[26] = {0}, record_t[26] = {0};
        for(int i=0; i<len_s;i++){
            record_s[s[i]-'a']++;
            record_t[t[i]-'a']++;
        }
        for(int i=0;i<26;i++){
            if(record_s[i]!=record_t[i])
                return false;
        }
        return true;        
    }
};
```


## string 为 unicode 编码
利用 map。
```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int len_s = s.size(), len_t = t.size();
        if(len_s != len_t)
            return false;
        
        map<char, int> record_s, record_t;
        map<char, int>::iterator it;
        
        for(int i=0;i<len_s;i++){
            it = record_s.find(s[i]);
            if(it != record_s.end())
                it->second++;
            else
                record_s.insert(pair<char, int>(s[i], 0));
        
            it = record_t.find(t[i]);
            if(it != record_t.end())
                it->second++;
            else
                record_t.insert(pair<char, int>(t[i], 0));         
        }
        
        for(it=record_s.begin();it!=record_s.end();it++){
            map<char, int>::iterator it2;
            it2 = record_t.find(it->first);
            
            if(it2==record_t.end() || it->second != it2->second)
                return false;
            record_t.erase(it2);
        }
        
        if(!record_t.empty())
            return false;
        
        return true;
        
    }
};
```

# 参考答案之一
排序。
```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        if(s==t)
            return true;
        return false;
    }
};
```