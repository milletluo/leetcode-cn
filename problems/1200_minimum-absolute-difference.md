## [题目描述(简单)](https://leetcode-cn.com/problems/minimum-absolute-difference/)
<div class="notranslate"><p>给你个整数数组&nbsp;<code>arr</code>，其中每个元素都 <strong>不相同</strong>。</p>

<p>请你找到所有具有最小绝对差的元素对，并且按升序的顺序返回。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>arr = [4,2,1,3]
<strong>输出：</strong>[[1,2],[2,3],[3,4]]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>arr = [1,3,6,10,15]
<strong>输出：</strong>[[1,3]]
</pre>

<p><strong>示例 3：</strong></p>

<pre><strong>输入：</strong>arr = [3,8,-10,23,19,-4,-14,27]
<strong>输出：</strong>[[-14,-10],[19,23],[23,27]]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>2 &lt;= arr.length &lt;= 10^5</code></li>
	<li><code>-10^6 &lt;= arr[i] &lt;= 10^6</code></li>
</ul>
</div>

## 思路
排序后遍历，最小绝对差一定出现在相邻两数间
再次遍历，两数差等于最小绝对差则加入输出数组

## 代码
```c++
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */

int cmp(const void *a, const void *b)
{
    return (*(int*)a - *(int*)b);
}

int** minimumAbsDifference(int* arr, int arrSize, int* returnSize, int** returnColumnSizes){
    int **output = NULL;
    int *retColSize = NULL;
    int count = 0;
    
    qsort(arr, arrSize, sizeof(int), cmp);
    int gapMin = arr[1] - arr[0];
    for (int i = 1; i < arrSize; i++) {
        int temp = abs(arr[i] - arr[i - 1]);
        if (gapMin == temp) {
            count++;
        } else if (gapMin > temp) {
            gapMin = temp;
            count = 1;
        }
    }
    *returnSize = count;
    output = (int**)malloc(sizeof(int*) * count);
    retColSize = (int*)malloc(sizeof(int) * count);
    for (int i = 0; i < count; i++) {
        output[i] = (int*)malloc(sizeof(int) * 2);
        retColSize[i] = 2;
    }
    int j = 0;
    for (int i = 0; i < arrSize - 1; i++) {
        if (abs(arr[i] - arr[i+1]) == gapMin) {
            output[j][0] = arr[i];
            output[j][1] = arr[i + 1];
            j++;
        }
    }
    *returnColumnSizes = retColSize;
    return output;
}
```