## [从前序与中序遍历序列构造二叉树(中等)](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
<div class="notranslate"><p>根据一棵树的前序遍历与中序遍历构造二叉树。</p>

<p><strong>注意:</strong><br>
你可以假设树中没有重复的元素。</p>

<p>例如，给出</p>

<pre>前序遍历 preorder =&nbsp;[3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]</pre>

<p>返回如下的二叉树：</p>

<pre>    3
   / \
  9  20
    /  \
   15   7</pre>
</div>

## 思路
前序遍历最先遍历根节点，中序遍历先遍历左子树；确定根节点在中序序列中的位置即可确认左子树和右子树的序列长度  
从而分别求出左子树的前序序列、左子树的中序序列、右子树的前序序列、右子树的中序序列  
递归求解

## 代码
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder == null || inorder == null || preorder.length == 0 || inorder.length == 0) {
            return null;
        }
        TreeNode root = new TreeNode(preorder[0]);
        // 确定根节点的位置
        int rootIndex = 0;
        for (int i = 0; i < inorder.length; i++) {
            if (preorder[0] == inorder[i]) {
                rootIndex = i;
                break;
            }
        }
        if (rootIndex != 0) {
            // 构造左子树的前序序列
            int[] lPre = new int[rootIndex];
            for (int i = 0; i < rootIndex; i++) {
                lPre[i] = preorder[i + 1];
            }
            // 构造左子树的中序序列
            int[] lIn = new int[rootIndex];
            for (int i = 0; i < rootIndex; i++) {
                lIn[i] = inorder[i];
            }
            root.left = buildTree(lPre, lIn);
        }

        int lenRight = preorder.length - rootIndex - 1;
        if (lenRight != 0) {
            // 构造右子树的前序序列
            int[] rPre = new int[lenRight];
            for (int i = 0; i < lenRight; i++) {
                rPre[i] = preorder[i + rootIndex + 1];
            }
            // 构造右子树的中序序列
            int[] rIn = new int[lenRight];
            for (int i = 0; i < lenRight; i++) {
                rIn[i] = inorder[i + rootIndex + 1];
            }
            root.right = buildTree(rPre, rIn);
        }

        return root;
    }
}
```
