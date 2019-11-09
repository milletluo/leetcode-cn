## [去除重复字母(困难))](https://leetcode-cn.com/problems/remove-duplicate-letters/)
<div class="notranslate"><p>给定一个仅包含小写字母的字符串，去除字符串中重复的字母，使得每个字母只出现一次。需保证返回结果的字典序最小（要求不能打乱其他字符的相对位置）。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> <code>"bcabc"</code>
<strong>输出:</strong> <code>"abc"</code>
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> <code>"cbacdcbc"</code>
<strong>输出:</strong> <code>"acdb"</code></pre>
</div>

## 思路
1. 统计各个字母出现的次数
2. 逐个遍历字母，如果当前字符字典序小于结果中的某字符x，且x在后续还会再出现，则将x从当前结果中剔除，将结果中已写标志清零
3. 将当前字典序最小的字符写入，并且置已写标志

## 代码
```c
#define ALPHANUM 26

char *removeDuplicateLetters(char *s)
{
    int count[ALPHANUM] = { 0 };
    int oriLen = strlen(s);
    int writed[ALPHANUM] = { 0 };
    char *out = (char *)malloc(sizeof(char) * (ALPHANUM + 1));

    // 统计各个字符出现次数
    for (int i = 0; i < oriLen; i++) {
        count[s[i] - 'a']++;
    }

    int ptr = 0;
    for (int i = 0; i < oriLen; i++) {
        int curIdx = s[i] - 'a';
        count[curIdx]--;
        // 如果结果中已经有该字符了（说明），跳过
        if (writed[curIdx] == 1) {
            continue;
        }
        // 如果当前字符字典序小于结果中的某字符x，且x在后续还会再出现，则将x从当前结果中剔除，将结果中已写标志清零
        // 这里其实就是栈的思想了，将字典序小的字符出栈
        while (ptr > 0 && s[i] < out[ptr - 1] && count[out[ptr - 1] - 'a'] > 0) {
            writed[out[ptr - 1] - 'a'] = 0;
            ptr--;
        }
        // 将当前字典序最小的字符写入，并且置已写标志
        writed[curIdx] = 1;
        out[ptr] = s[i];
        ptr++;
    }
    out[ptr] = '\0';
    return out;
}
```
