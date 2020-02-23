## [二叉树的右视图(中等)](https://leetcode-cn.com/problems/binary-tree-right-side-view/)
<div class="notranslate"><p>给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong>&nbsp;[1,2,3,null,5,null,4]
<strong>输出:</strong>&nbsp;[1, 3, 4]
<strong>解释:
</strong>
   1            &lt;---
 /   \
2     3         &lt;---
 \     \
  5     4       &lt;---
</pre>
</div>

## 思路
层序遍历，广度优先搜索，借助队列  
思路1：当全局队列不为空时，先临时记录下一层的所有节点，然后记录该层最后更新的值，既最右值，再将下一层的所有节点放入全局队列

思路2：记录下当前队列中元素的个数，作为当前层需要遍历的次数

## 代码1
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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) {
            return res;
        }
        Queue<TreeNode> allNode = new LinkedList<>();
        allNode.add(root);
        while (!allNode.isEmpty()) {
            Queue<TreeNode> nextlvlNode = new LinkedList<>();
            int lastVal = 0;
            // 临时记录下一整层的所有元素
            while (!allNode.isEmpty()) {
                TreeNode temp = allNode.remove();
                lastVal = temp.val;
                if(temp.left != null) {
                    nextlvlNode.add(temp.left);
                }
                if(temp.right != null) {
                    nextlvlNode.add(temp.right);
                }
            }
            // 记录本层最后更新的值，既最右值
            res.add(lastVal);
            allNode.addAll(nextlvlNode);
        }
        return res;
    }
}
```

## 代码2
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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) {
            return res;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int count = queue.size();
            // 记录当前层需要遍历的次数
            while (count > 0) {
                TreeNode temp = queue.remove();
                count--;
                if (count == 0) {
                    res.add(temp.val);
                }
                if(temp.left != null) {
                    queue.add(temp.left);
                }
                if(temp.right != null) {
                    queue.add(temp.right);
                }
            }
        }
        return res;
    }
}
```
