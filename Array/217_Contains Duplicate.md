# [217.Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

# 思路
把nums里的元素一个个放到set里，如果set已有该元素则返回true，全部放完之后返回false。
也可以先排序，再遍历排序好的算法里前后有无重复的。
但冒泡排序时间复杂度太高未通过，利用O(nlogn)的算法就没问题。

# C++
```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        set<int> s;
        set<int>::iterator s_it;
        for(vector<int>::iterator v_it=nums.begin();v_it!=nums.end();v_it++){
            s_it = s.find(*v_it);
            if(s_it!=s.end()) return true;
            s.insert(*v_it);
        }
        return false;
    }  
};
```