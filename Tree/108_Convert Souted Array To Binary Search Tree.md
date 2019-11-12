# [108.Convert Souted Array To Binary Search Tree](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)



```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        int len = nums.size();
        if(len==1){
            return new TreeNode(nums[0]);
        }
        if(len==0)
            return NULL;
        
        vector<int> left_nums(nums.begin(), nums.begin()+len/2);  // 第num.begin()+len/2个数不在其中
        vector<int> right_nums(nums.begin()+len/2+1, nums.end());
        TreeNode *root = new TreeNode(nums[len/2]);
        root->left = sortedArrayToBST(left_nums);
        root->right = sortedArrayToBST(right_nums);
        return root;
    }
};
```