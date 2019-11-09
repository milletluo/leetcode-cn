## [回文对(困难))](https://leetcode-cn.com/problems/palindrome-pairs/)
<div class="notranslate"><p>给定一组<strong>唯一</strong>的单词， 找出所有<strong><em>不同&nbsp;</em></strong>的索引对<code>(i, j)</code>，使得列表中的两个单词，&nbsp;<code>words[i] + words[j]</code>&nbsp;，可拼接成回文串。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入: </strong>["abcd","dcba","lls","s","sssll"]
<strong>输出: </strong>[[0,1],[1,0],[3,2],[2,4]] 
<strong>解释: </strong>可拼接成的回文串为 <code>["dcbaabcd","abcddcba","slls","llssssll"]</code>
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入: </strong>["bat","tab","cat"]
<strong>输出: </strong>[[0,1],[1,0]] 
<strong>解释: </strong>可拼接成的回文串为 <code>["battab","tabbat"]</code></pre>
</div>

## 思路
暴力法，遍历、拼接后判断是否是回文串
判断方法做优化，否则超时

## 代码
```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
bool CanBePalindrome(char *a, char *b)
{
    int len = strlen(a) + strlen(b);
    char *combine = (char*)malloc(sizeof(char) * (len + 1));
    memset(combine, 0, len + 1);
    strcat(combine, a);
    strcat(combine, b);
    // printf("%s = %s + %s\n", combine, a, b);
    int left = 0;
    int right = len - 1;
    while (left < right) {
        if (combine[left] != combine[right]) {
            free(combine);
            return false;
        }
        left++;
        right--;
    }
    free(combine);
    return true;
}

int** palindromePairs(char ** words, int wordsSize, int* returnSize, int** returnColumnSizes)
{
    int **res = NULL;
    int *retColSizes = NULL;
    int count = 0;
    int len[10000] = {0};
    res = (int **)malloc(sizeof(int*) * 10000);
    for (int i = 0; i < 10000; i++) {
        res[i] = (int *)malloc(sizeof(int) * 2);
    }
    int left, right, lenI, lenJ;
    for (int i = 0; i < wordsSize; i++) {
        for (int j = 0; j < wordsSize; j++) {
            // printf("-----%d = %s, %d = %s\n", i, words[i], j, words[j]);
            /* 调用str函数拼装后遍历判断超时 */
            // if ((i != j) && CanBePalindrome(words[i], words[j])) {
            //     res[count][0] = i;
            //     res[count][1] = j;
            //     count++;
            // }
            if (i == 0) {
                len[j] = strlen(words[j]);
            }
            if (i == j) {
                continue;
            }
            for (lenI = len[i], lenJ = len[j], left = 0, right = lenI + lenJ - 1; left <= right; left++, right--) {
                // 三目运算符要单独括起来
                if (((left < lenI) ? words[i][left] : words[j][left - lenI]) != 
                    ((right < lenI) ?  words[i][right] : words[j][right - lenI])) {
                    break;
                }
            }
            if (left >= right) {
                res[count][0] = i;
                res[count][1] = j;
                count++;
            }
        }
    }
    retColSizes = (int*)malloc(sizeof(int) * count);
    for (int i = 0; i < count; i++) {
        retColSizes[i] = 2;
    }
    *returnSize = count;
    *returnColumnSizes = retColSizes;
    return res;
}
```
