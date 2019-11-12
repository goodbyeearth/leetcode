# [53.Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

# 思路
遍历一遍即可解决，假设遍历至当前数，为第 i 个。判断以第 i-1 个数结尾的最大子序列和为正或负，
若为正则加上当前数得到以第 i 个数结尾的最大子序列和；若为负则以当前数为以第 i 个数结尾的最大子序列和。
在 n 个以上求得结果中，找到最大的最大子序列和。

# C++
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int preMaxSubSum = nums[0];
        int maxSubSum = preMaxSubSum;
        for(int i=1;i<nums.size();i++){
            if(preMaxSubSum<=0)
                preMaxSubSum = nums[i];
            else
                preMaxSubSum += nums[i];
            if(maxSubSum < preMaxSubSum)
                maxSubSum = preMaxSubSum;
        }
        return maxSubSum;
    }
};
```