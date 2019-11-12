# [66.Plus One](https://leetcode-cn.com/problems/plus-one/)

```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        vector<int> res;
        int temp=1;
        for(int i=digits.size()-1;i>=0;i--){
            int d = digits[i]+temp;
            if(d<10)
                temp=0;
            else{
                d = 0;
                temp=1;
            }
            res.push_back(d);
        }
        if(temp==1)
            res.push_back(1);
        reverse(res.begin(), res.end());
        return res;
    }
};
```