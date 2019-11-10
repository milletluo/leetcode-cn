## [字母异位词分组(中等)](https://leetcode-cn.com/problems/group-anagrams/)
<div class="notranslate"><p>给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> <code>["eat", "tea", "tan", "ate", "nat", "bat"]</code>,
<strong>输出:</strong>
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]</pre>

<p><strong>说明：</strong></p>

<ul>
	<li>所有输入均为小写字母。</li>
	<li>不考虑答案输出的顺序。</li>
</ul>
</div>

## 思路
1. 先按字典序排序，短的在前，同长的小的在前
2. 根据每个字母出现的次数判断是否是异位词
3. 逐个遍历，因为已经排序，所以可以根据同组当中最后一个异位词的位置更新遍历的下标，加快遍历速度

## 代码
```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
 #define WORD_NUMS 50
 #define WORD_SIZE 30

int cmp(const void *aa, const void *bb)
{
    char *a = *(char**)aa;
    char *b = *(char**)bb;
    int aLen = strlen(a);
    int bLen = strlen(b);
    int aFlag[26] = {0};
    int bFlag[26] = {0};
    if (aLen != bLen) {
        return aLen - bLen; // 短的在前
    } else {
        // 记录每个字母出现的次数，出现少的在前
        for (int i = 0; i < aLen; i++) {
            aFlag[a[i] - 'a']++;
        }
        for (int i = 0; i < bLen; i++) {
            bFlag[b[i] - 'a']++;
        }
        for (int i = 0; i < 26; i++) {
            if (aFlag[i] != bFlag[i]) {
                return aFlag[i] - bFlag[i];
            }
        }
    }
    return 0;
}

char *** groupAnagrams(char ** strs, int strsSize, int* returnSize, int** returnColumnSizes){
    if (strs == NULL || strsSize == 0) {
        *returnSize = 0;
        return NULL;
    }
    int *retColSize = (int *)malloc(sizeof(int) * strsSize);
    char ***res = (char ***)malloc(sizeof(char **) * strsSize);
    for (int i = 0; i < strsSize; i++) {
        res[i] = (char **)malloc(sizeof(char *) * WORD_NUMS);
        for (int j = 0; j < WORD_NUMS; j++) {
            res[i][j] = (char*)malloc(sizeof(char) * WORD_SIZE);
        }
    }
    qsort(strs, strsSize, sizeof(char*), cmp); // 先按字典序排序，短的在前，同长的小的在前
    int count = 0;
    int idx;
    for (int i = 0; i < strsSize;) {
        idx = strsSize;
        for (int j = i + 1; j < strsSize; j++) {
            // 依次遍历，如果不是异位词，跳出
            if (cmp(strs + i, strs + j) != 0) {
                idx = j;
                break;
            }
        }
        // 如果找到非异位词，将前面的异位词依次拷贝到结果中，更新下次遍历的位置为非异位词的位置
        for (int j = 0; j < idx - i; j++) {
            // res[count][j] = strs[i + j];
            strcpy(res[count][j], strs[i + j]);
        }
        retColSize[count] = idx - i;
        i = idx;
        count++;
    }
    *returnSize = count;
    *returnColumnSizes = retColSize;
    return res;
}
```
