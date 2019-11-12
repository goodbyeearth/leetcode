# [8.String To Integer Atoi](https://leetcode-cn.com/problems/string-to-integer-atoi/)

# 我的答案
使用 double 来存储累加的数，以便判断是否越界，用 float 的话当数据较大时，转化为 int 型会出问题。

```c++
class Solution {
public:
    int myAtoi(string str) {
        int i=0;
        double res=0;
        double bound;
        char sign;
        
        while(i<str.size() && str[i]==' ')
            i++;
        if(i==str.size())
            return 0;
        
        if(str[i]=='+' || str[i]=='-' || (str[i]>='0' && str[i]<='9')){
            if(str[i]=='-'){
                sign = '-';
                bound = -(double)INT_MIN;
            }
            else{
                sign = '+';
                bound = (double)INT_MAX;
            }
                
            
            if(str[i]=='+'||str[i]=='-'){
                i++;
                if(i==str.size() || str[i]<'0'||str[i]>'9')
                    return 0;  
            }
        }
        else
            return 0;
            
        while(i<str.size() && str[i]>='0' && str[i]<='9'){
            res = res*10 + (str[i]-'0');
            if(res>bound){
                if(sign=='+')
                    return INT_MAX;
                else
                    return INT_MIN;
            }
            i++;
        }
        if(sign=='+')
            return (int)res;
        else
            return (int)(-res);
        
    }
};
```

# 简洁的答案
```c++
class Solution {
public:
    int myAtoi(string str) {
        int i=0;
        long res=0;
        int sign=1;
        while(i<str.size() && str[i]==' ') ++i;
        if(i == str.size()) return 0;
        if(str[i]=='-') {sign=-1;i++;}
        else if(str[i]=='+') i++;          
        while(i<str.size() && isdigit(str[i]))
        {
            res=res*10+(str[i++]-'0');
            if(res>INT_MAX){
                if(sign==1) return INT_MAX;
                else return INT_MIN;
            }
        }
        return res*sign;
    }
};
```
作者：li-ming-hui-2
链接：https://leetcode-cn.com/problems/two-sum/solution/c-by-li-ming-hui-2/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
