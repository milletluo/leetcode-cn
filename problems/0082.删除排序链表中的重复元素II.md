## [删除排序链表中的重复元素 II(中等)](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)
<div class="notranslate"><p>给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中&nbsp;<em>没有重复出现&nbsp;</em>的数字。</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入:</strong> 1-&gt;2-&gt;3-&gt;3-&gt;4-&gt;4-&gt;5
<strong>输出:</strong> 1-&gt;2-&gt;5
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> 1-&gt;1-&gt;1-&gt;2-&gt;3
<strong>输出:</strong> 2-&gt;3</pre>
</div>

## 思路
1. 记录当前节点和上一节点，如果当前节点和下一节点相等，直接将上一节点的下一节点指向下一节点的下一节点
2. 首部相同和尾部相同的情况特殊处理

## 代码
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* deleteDuplicates(struct ListNode* head){
    if (head == NULL) {
        return NULL;
    }
    struct ListNode *preNode = NULL;
    struct ListNode *curNode = head;
    while (curNode->next != NULL) {
        if(curNode->val != curNode->next->val) {
            preNode = curNode;
            curNode = curNode->next;
            continue;
        }
        while (curNode->next != NULL && curNode->val == curNode->next->val) {
            curNode = curNode->next;
        }
        // 尾部相同
        if (curNode->next == NULL) {
            // 首部相同
            if (preNode == NULL) {
                return NULL;
            }
            preNode->next = NULL;
            break;
        } else {
            // 首部相同
            if (preNode == NULL) {
                head = curNode->next;
            } else {
                preNode->next = curNode->next;
            }
            curNode = curNode->next;
        }
    }
    return head;
}
```
## 代码（递归）
```c
struct ListNode* deleteDuplicates(struct ListNode* head){
    if (head == NULL || head->next == NULL) {
        return head;
    }
    struct ListNode *next = head->next;
    //如果是这种情况
    //      1 --> 1 --> 1 --> 2 --> 3
    //     head  next
    //1.则需要移动next直到出现与当前head.value不相等的情况（含null）
    if (head->val == next->val) {
        while (next != NULL && head->val == next->val) {
            next = next->next;
        }
        //2.并且此时的head已经不能要了，因为已经head是重复的节点
        head = deleteDuplicates(next);
    } else {
        //3.如果没有出现1的情况，则递归返回的节点就作为head的子节点
        head->next = deleteDuplicates(next);
    }
    return head;
}
```