# [136. Single Number](https://leetcode.com/problems/single-number/)

# 思路1
异或。空间复杂度 O(1)，时间复杂度 O(n)。

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = nums[0];
        for(int i=1;i<nums.size();i++){
            res ^= nums[i];
        }
        return res;
    }
};
```

