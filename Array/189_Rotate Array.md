# [63.Rotate Array](https://leetcode-cn.com/problems/rotate-array/)

# 思路

## 思路1
做三次 reverse

## C++
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int len = nums.size();
        k = k%len;
        if(k==0){
            return;
        }
        reverse(nums, 0, len-k-1);
        reverse(nums, len-k, len-1);
        reverse(nums, 0 , len-1);
    }
    void reverse(vector<int>& nums, int i, int j){
        while(i<j){
            swap(nums[i++], nums[j--]);
        }
    }
};
```


## 思路2
第0到k-1的数跟后面k到2k-1的数交换，
然后再将0到k-1的数跟2k到3k-1的数交换...重复知道后面的所有数交换完毕。
若此时刚好交换完成则退出。
否则对前面的k个数做上述类似的操作，相应的步长k需要做改变。

## 踩坑
k 需要对数组长度取模，若结果为0则需要直接 return。

## C++
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int len = nums.size();
        if(k%len==0){
            return;
        }   
        int step = k;
        if(step > len){
            step = step % len;
        }

        int i = 0, j;
        j = i + step;
        while(1){
            while(j <= len-1){
                swap(nums[i], nums[j]);
                i = (i+1) % step;
                j++;
            }
            if(i==0)
                break;
            else{
                len = step;
                step = step - i;
                i = 0;
                j = i + step;          
            }
            
        }
    }
};
```

