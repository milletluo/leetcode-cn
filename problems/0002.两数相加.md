## [两数相加(中等)](https://leetcode-cn.com/problems/add-two-numbers/)
<div class="notranslate"><p>给出两个&nbsp;<strong>非空</strong> 的链表用来表示两个非负的整数。其中，它们各自的位数是按照&nbsp;<strong>逆序</strong>&nbsp;的方式存储的，并且它们的每个节点只能存储&nbsp;<strong>一位</strong>&nbsp;数字。</p>

<p>如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。</p>

<p>您可以假设除了数字 0 之外，这两个数都不会以 0&nbsp;开头。</p>

<p><strong>示例：</strong></p>

<pre><strong>输入：</strong>(2 -&gt; 4 -&gt; 3) + (5 -&gt; 6 -&gt; 4)
<strong>输出：</strong>7 -&gt; 0 -&gt; 8
<strong>原因：</strong>342 + 465 = 807
</pre>
</div>

## 思路
链表存的数据本来就是低位在前，直接相加，处理好进位、长度不一样就行

## 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }

        ListNode node = new ListNode(-1);
        ListNode res = node;
        int upFlag = 0;
        while (l1 != null && l2 != null) {
            int sum = l1.val + l2.val + upFlag;
            node.next = new ListNode(sum % 10);
            upFlag = sum / 10;
            node = node.next;
            l1 = l1.next;
            l2 = l2.next;
        }
        while (l1 != null) {
            int sum = l1.val + upFlag;
            node.next = new ListNode(sum % 10);
            upFlag = sum / 10;
            node = node.next;
            l1 = l1.next;
        }
        while (l2 != null) {
            int sum = l2.val + upFlag;
            node.next = new ListNode(sum % 10);
            upFlag = sum / 10;
            node = node.next;
            l2 = l2.next;
        }
        if (upFlag == 1) {
            node.next = new ListNode(1);
        }
        return res.next;
    }
}
```
