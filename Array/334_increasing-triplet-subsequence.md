# [334. increasing-triplet-subsequence](https://leetcode-cn.com/problems/increasing-triplet-subsequence/)

# 方法1：
利用min记下最小值，mid记下第2小，如果有另一个数比mid大，则存在递增三元组。
```
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int min, mid=INT_MAX;
        if(nums.size()<3)
            return false;
        min = nums[0];
        for(int i=1; i<nums.size(); i++){
            if(nums[i]<min)
                min = nums[i];       // 记下最新的最小的数
            else if((nums[i]>min) && (nums[i]<mid))
                mid = nums[i];
            else if(nums[i]>mid)
                return true;
        }
        return false;
    }
};
```