# [326.Power Of Three](https://leetcode-cn.com/problems/power-of-three/)

# 递归
```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n==0)
            return false;
        if(n==1)
            return true;
        if(n%3==0)
            return isPowerOfThree(n/3);
        else
            return false;
    }
};
```
# 循环
```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n==0)
            return false;
        while(n!=1){
            if(n%3!=0)
                return false;
            n = n/3;
        }
        return true;
    }
};
```


