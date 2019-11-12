# [1. Two Sum](https://leetcode-cn.com/problems/two-sum/)

# 思路
建立一个 map, 扫描nums，若target-nums[i]在 map 里，返回 map 对应的 value 和 i；
若不在 map 里，则把 nums[i]：i 存到 map 里。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> res;
        map<int, int> m;
        for(int i=0;i<nums.size();i++){
            if(m.count(target-nums[i])){
                res.push_back(m[target-nums[i]]);
                res.push_back(i);
                return res;
            }
            else{
                m.insert(pair<int, int>(nums[i], i));
            }
        }
        return res;
    }
};
```