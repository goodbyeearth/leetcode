# [105. 从前序与中序遍历序列构造二叉树] (https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

# 方法1
利用递归，
将前序数组的第一个元素作为划分点，把中序数组划分为两组：左边的是左子树的中序数组，长度为a，右边的是右子树的中序数组，长度为b。
前序的第二个元素开始往后 a 个元素作为左子树的前序数组，往后剩下的作为右子树的前序数组。

```
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(preorder.size()==0)
            return NULL;
        return helper(preorder, 0, preorder.size()-1, inorder, 0, inorder.size()-1);
    }
    TreeNode* helper(vector<int>& preorder, int s1, int t1, vector<int>& inorder, int s2, int t2){
        int v = preorder[s1];
        TreeNode *p = new TreeNode(v);
        int k=0;
        while(inorder[s2+k]!=v)
            k++;
        if(k>0)
            p->left = helper(preorder, s1+1, s1+k, inorder, s2, s2+k-1);
        if(s2+k<t2)
            p->right = helper(preorder, s1+k+1, t1, inorder, s2+k+1, t2);
        return p;
    }
};
```