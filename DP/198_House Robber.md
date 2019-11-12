# [198.House Robber](https://leetcode-cn.com/problems/house-robber/)

# 思路
用一个等长数组 m 来存储截止到当前位置的最大和。
假设 m[0~i-1] 均已求出，则 m[i] 等于 max(m[i-3]+nums[i], m[i-2]+nums[i])。
题目的要求是不能相邻，即跳过 m[i-1]。
最后只要返回数组 m 的最后两个元素中最大元素即可。

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size()==0)
            return 0;
        else if(nums.size()==1)
            return nums[0];
        else if(nums.size()==2)
            return max(nums[0], nums[1]);
        else if(nums.size()==3)
            return max(nums[1], nums[0]+nums[2]);
        
        int m1, m2, m3, m4;
        m1 = nums[0];
        m2 = nums[1];
        m3 = nums[2]+nums[0];
        
        for(int i=3;i<nums.size();i++){
            m4 = max(m1+nums[i], m2+nums[i]);
            m1=m2; m2=m3; m3=m4;
        }
        return max(m2, m3); 
    }
};
```

# 别人的答案
对于第i户人家，

如果偷这一家，则相邻的第i-1户就不能偷，所以最多投dp[i-2]+nums[i-1](nums数组从0开始)；

如果不偷这一家，则从第0到第i户人家最多能获得dp[i-1]的财物

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        int sLen=nums.size();
        if(sLen==0)return 0;
        if(sLen==1)return nums[0];
        vector<int> dp(sLen+1,0);
        dp[1] = nums[0];
        for(int i=2;i<=sLen;i++)
            dp[i]=max(dp[i-1],dp[i-2]+nums[i-1]);
        return dp[sLen];
    }
};
```
作者：LukeLee
链接：https://leetcode-cn.com/problems/two-sum/solution/10xing-dong-tai-gui-hua-c-beats-969-in-4ms-by-luke/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。