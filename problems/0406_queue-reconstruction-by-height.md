## [题目描述(中等)](https://leetcode-cn.com/problems/queue-reconstruction-by-height/)
<div class="notranslate"><p>假设有打乱顺序的一群人站成一个队列。 每个人由一个整数对<code>(h, k)</code>表示，其中<code>h</code>是这个人的身高，<code>k</code>是排在这个人前面且身高大于或等于<code>h</code>的人数。 编写一个算法来重建这个队列。</p>

<p><strong>注意：</strong><br>
总人数少于1100人。</p>

<p><strong>示例</strong></p>

<pre>输入:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

输出:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
</pre>
</div>

## 思路
由矮到高依次排位，同等高度的，先排需要留空位多的，即k较大的，始终在前方留k个空位

## 代码
```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int cmp(const void *aa, const void *bb)
{
    int *a = *(int**)aa;
    int *b = *(int**)bb;
    if (a[0] == b[0]) {
        return b[1] - a[1];
    } else {
        return a[0] - b[0];
    }
}

int** reconstructQueue(int** people, int peopleSize, int* peopleColSize, int* returnSize, int** returnColumnSizes){
    // 从矮到高排序，若身高相同，k大的排前面，先处理
    qsort(people, peopleSize, sizeof(int*), cmp);
    int **out = NULL;
    out = (int**)malloc(sizeof(int*) * peopleSize);
    for (int i = 0; i < peopleSize; i++) {
        out[i] = (int*)malloc(sizeof(int) * 2);
    }
    int flag[1100] = {0}; // 记录该位置是否已排人
    *returnSize = peopleSize;
    *returnColumnSizes = peopleColSize;
    for (int i = 0; i < peopleSize; i++) {
        int insertIdx = 0;
        int index = people[i][1] + 1;
        // 找出第k个没排人的位置
        while (index > 0) {
            if (flag[insertIdx] == 0) {
                index--;
            }
            insertIdx++;
        }
        printf("%d:[%d %d], %d\n", i, people[i][0], people[i][1], insertIdx - 1);
        out[insertIdx - 1][0] = people[i][0];
        out[insertIdx - 1][1] = people[i][1];
        flag[insertIdx - 1] = 1;
    }
    return out;
}
```
