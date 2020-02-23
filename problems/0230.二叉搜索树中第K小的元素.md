## [二叉搜索树中第K小的元素(中等)](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)
<div class="notranslate"><p>给定一个二叉搜索树，编写一个函数&nbsp;<code>kthSmallest</code>&nbsp;来查找其中第&nbsp;<strong>k&nbsp;</strong>个最小的元素。</p>

<p><strong>说明：</strong><br>
你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
&nbsp;  2
<strong>输出:</strong> 1</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
<strong>输出:</strong> 3</pre>

<p><strong>进阶：</strong><br>
如果二叉搜索树经常被修改（插入/删除操作）并且你需要频繁地查找第 k 小的值，你将如何优化&nbsp;<code>kthSmallest</code>&nbsp;函数？</p>
</div>

## 思路
因为是二叉搜索树，所以中序遍历出来即为排好序的序列

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
    List<Integer> res = new ArrayList<>();
    public int kthSmallest(TreeNode root, int k) {
        inorder(root);
        return res.get(k - 1);
    }
    private void inorder(TreeNode root) {
        if(root == null) {
            return;
        }
        inorder(root.left);
        res.add(root.val);
        inorder(root.right);
    }
}
```
