# [283.Move Zeroes](https://leetcode-cn.com/problems/move-zeroes/)
# 答案
非零元素往前填，覆盖零的元素，记录零的个数，最后补上所有零。
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int i=0, zero_count=0;
        while(i<nums.size()){
            nums[i-zero_count] = nums[i];
            if(nums[i]==0)
                zero_count++;
            i++;
        }
        int len = nums.size();
        while(zero_count>0){
            nums[len-zero_count] = 0;
            zero_count--;
        }
        return;
    }
};
```

# 我的答案（太慢）
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int index_zero=0, zero_set, j;
        bool zero_found;
        while(index_zero<nums.size() && nums[index_zero]!=0)
            index_zero++;
        if(index_zero==nums.size())   //无0
            return;
        
        zero_set = 0;     // 已经排好的0的个数
               
        while(true){
            if(index_zero==-1){     // 无0或所有0都已排好
                return;
            }
            j = index_zero;
            index_zero=-1;
            zero_found = false;
            while(j+1<nums.size()-zero_set){
                if(nums[j+1]==0 && !zero_found){
                    zero_found = true;
                    index_zero = j;
                }
                swap(nums[j],nums[j+1]);
                j++;
            }
            zero_set++;
        }
    }
};
```