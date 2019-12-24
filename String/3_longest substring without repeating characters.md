# 方法 1
相对暴力。对所有n个元素进行遍历做以下操作：找到以该元素为起点的最长子串，用一个 set 来记录。
输出这 n 个子串的最长长度
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        set<char> substring;
        int max_len = 0;
        for(int i=0; i<s.size();i++){
            substring.clear();
            substring.insert(s[i]);
            for(int j=i+1; j<s.size(); j++){
                if(substring.find(s[j])==substring.end())
                    substring.insert(s[j]);
                else
                    break;
            }
            if(max_len<substring.size()){
                max_len = substring.size();
            }
        }
        return max_len;
    }
};
```

# 方法2
稍快，是方法1的改进。无需遍历n个元素找到以其开始的子串最长长度，用 tail 指针逐个元素遍历，看head 到 tail 的这一子串是否存在重复字符，若不重复则增加tail，否则将 head 置为重复字符后面的那一位。
因为在此之前的任一字符开始的子串长度不可能大于当前记录的最长子串长度。
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        set<char> substring;
        int max_len = 0, current_len = 1;
        int head=0, tail=1;
        if(s.size()<=1)
            return s.size();
        substring.insert(s[head]);
        while(tail<s.size()){
            if(substring.find(s[tail]) == substring.end()){  // 不重复
                substring.insert(s[tail]);
                tail++;       
            }
            else{
                while(s[head] != s[tail]){  // 找到子串中被重复的字符
                    substring.erase(s[head]);      // 去除被重复字符之前的所有字符
                    head++;
                }
                substring.erase(s[head]);  
                head++;
            }
            if(substring.size()>max_len){
                max_len = substring.size();
            }
        }
        return max_len;
    }
};
```

# 方法3
比上述两种快，用map来存储某一个字符在字符串中最后出现的位置，用 tail 指针遍历字符串。
只要 s[tail]出现在[head, tail-1] 的子串中，假设出现的位置是 p，则把 head 置为 p+1。
```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        map<char, int> posmap;
        map<char, int>::iterator p;
        int max_len = 0;
        int head=0, tail=0;
        while(tail<s.size()){
            p = posmap.find(s[tail]);
            if(p!=posmap.end() && p->second>=head){    //s[tail]在 [head, tail-1] 的子串中
                head = p->second+1;
            }
            posmap[s[tail]] = tail;
            tail++;
            if(tail-head>max_len)
                max_len = tail-head;
        }
        return max_len;
    }
};
```