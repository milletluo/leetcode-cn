## [按奇偶排序数组(简单)](https://leetcode-cn.com/problems/sort-array-by-parity/)
<div class="notranslate"><p>给定一个非负整数数组 <code>A</code>，返回一个数组，在该数组中，&nbsp;<code>A</code> 的所有偶数元素之后跟着所有奇数元素。</p>

<p>你可以返回满足此条件的任何数组作为答案。</p>

<p>&nbsp;</p>

<p><strong>示例：</strong></p>

<pre><strong>输入：</strong>[3,1,2,4]
<strong>输出：</strong>[2,4,3,1]
输出 [4,2,3,1]，[2,4,1,3] 和 [4,2,1,3] 也会被接受。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>1 &lt;= A.length &lt;= 5000</code></li>
	<li><code>0 &lt;= A[i] &lt;= 5000</code></li>
</ol>
</div>

## 思路
左指针遍历奇数，右指针遍历偶数，同时遍历到时交换

## 代码
```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* sortArrayByParity(int* A, int ASize, int* returnSize){
    int *res = (int *)malloc(sizeof(int) * ASize);
    for (int i = 0; i < ASize; i++) {
        res[i] = A[i];
    }
    *returnSize = ASize;
    int left = 0;
    int right = ASize - 1;
    int temp;
    while (left < right) {
        if ((res[left] % 2 == 1) && (res[right] % 2 == 0)) {
            temp = res[left];
            res[left] = res[right];
            res[right] = temp;
        }
        if (res[left] % 2 == 0) {
            left++;
        }
        if (res[right] % 2 == 1) {
            right--;
        }
    }
    return res;
}
```
