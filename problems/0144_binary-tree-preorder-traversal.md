## [二叉树的前序遍历(中等)](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
<div class="notranslate"><p>给定一个二叉树，返回它的&nbsp;<em>前序&nbsp;</em>遍历。</p>

<p>&nbsp;<strong>示例:</strong></p>

<pre><strong>输入:</strong> [1,null,2,3]  
   1
    \
     2
    /
   3 

<strong>输出:</strong> [1,2,3]
</pre>

<p><strong>进阶:</strong>&nbsp;递归算法很简单，你可以通过迭代算法完成吗？</p>
</div>

## 思路
1. 递归法，主要是将指针和下标作为迭代函数的入参传入
2. 迭代法，用一个栈保存中间节点，以便再处理完左叶子后能找到右叶子

## 代码
```c
#define TREE_SIZE 1000

typedef struct {
    struct TreeNode *treeNodes[TREE_SIZE];
    int size;
}Stack;

void Preorder(const struct TreeNode *root, int *resArray, int *idx)
{
    if (root) {
        resArray[(*idx)++] = root->val;
        Preorder(root->left, resArray, idx);
        Preorder(root->right, resArray, idx);
    }
}

void PreorderWithStack(struct TreeNode *root, int *resArray, int *idx)
{
    struct TreeNode *tempNode = root;
    Stack nodeStack;
    nodeStack.size = 0;
    while ((tempNode != NULL) || (nodeStack.size != 0)) {
        while (tempNode) {
            resArray[(*idx)++] = tempNode->val; // 前序遍历，先处理根节点，再处理左节点
            nodeStack.treeNodes[nodeStack.size++] = tempNode; // 把父节点压栈存起来，先处理左子树
            tempNode = tempNode->left;
        }
        if (nodeStack.size != 0) {
            tempNode = nodeStack.treeNodes[--nodeStack.size]; // 如果还有父节点没处理完，取出父节点，取其右子树
            tempNode = tempNode->right;
        }
    }
}

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* preorderTraversal(struct TreeNode* root, int* returnSize)
{
    int *res = (int*)malloc(sizeof(int) * TREE_SIZE);
    if (res == NULL) {
        return NULL;
    }
    memset(res, 0, TREE_SIZE);
    *returnSize = 0;
    PreorderWithStack(root, res, returnSize);
    return res;
}
```
