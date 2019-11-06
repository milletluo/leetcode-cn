## [对链表进行插入排序(中等)](https://leetcode-cn.com/problems/insertion-sort-list/)
<div class="notranslate"><p>对链表进行插入排序。</p>

<p><img src="https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif" alt=""><br>
<small>插入排序的动画演示如上。从第一个元素开始，该链表可以被认为已经部分排序（用黑色表示）。<br>
每次迭代时，从输入数据中移除一个元素（用红色表示），并原地将其插入到已排好序的链表中。</small></p>

<p>&nbsp;</p>

<p><strong>插入排序算法：</strong></p>

<ol>
	<li>插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。</li>
	<li>每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。</li>
	<li>重复直到所有输入数据插入完为止。</li>
</ol>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> 4-&gt;2-&gt;1-&gt;3
<strong>输出:</strong> 1-&gt;2-&gt;3-&gt;4
</pre>

<p><strong>示例&nbsp;2：</strong></p>

<pre><strong>输入:</strong> -1-&gt;5-&gt;3-&gt;4-&gt;0
<strong>输出:</strong> -1-&gt;0-&gt;3-&gt;4-&gt;5
</pre>
</div>

## 思路
注意指针操作

## 代码
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

struct ListNode* insertionSortList(struct ListNode* head){
    if (head == NULL) {
        return NULL;
    }
    struct ListNode *beginNode = head;
    struct ListNode *endNode = head;
    struct ListNode *curNode = head->next;
    while (curNode != NULL) {
        // 插在最后
        if (curNode->val >= endNode->val) {
            endNode = curNode;
            curNode = curNode->next;
            continue;
        }
        // 插在最前
        if (curNode->val < beginNode->val) {
            endNode->next = curNode->next;
            curNode->next = beginNode;
            beginNode = curNode;
            curNode = endNode->next;
            continue;
        }
        // 插在中间
        struct ListNode *insertNode = beginNode;
        while (insertNode != curNode) {
            if (curNode->val >= insertNode->val && curNode->val < insertNode->next->val) {
                endNode->next = curNode->next;
                curNode->next = insertNode->next;
                insertNode->next = curNode;
                curNode = endNode->next;
                break;
            } else {
                insertNode = insertNode->next;
            }
        }
    }
    head = beginNode;
    return head;
}
```
