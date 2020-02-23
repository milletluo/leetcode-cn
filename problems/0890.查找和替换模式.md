## [查找和替换模式(中等)](https://leetcode-cn.com/problems/find-and-replace-pattern/)
<div class="notranslate"><p>你有一个单词列表&nbsp;<code>words</code>&nbsp;和一个模式&nbsp;&nbsp;<code>pattern</code>，你想知道 <code>words</code> 中的哪些单词与模式匹配。</p>

<p>如果存在字母的排列 <code>p</code>&nbsp;，使得将模式中的每个字母 <code>x</code> 替换为 <code>p(x)</code> 之后，我们就得到了所需的单词，那么单词与模式是匹配的。</p>

<p><em>（回想一下，字母的排列是从字母到字母的双射：每个字母映射到另一个字母，没有两个字母映射到同一个字母。）</em></p>

<p>返回 <code>words</code> 中与给定模式匹配的单词列表。</p>

<p>你可以按任何顺序返回答案。</p>

<p>&nbsp;</p>

<p><strong>示例：</strong></p>

<pre><strong>输入：</strong>words = ["abc","deq","mee","aqq","dkd","ccc"], pattern = "abb"
<strong>输出：</strong>["mee","aqq"]
<strong>解释：
</strong>"mee" 与模式匹配，因为存在排列 {a -&gt; m, b -&gt; e, ...}。
"ccc" 与模式不匹配，因为 {a -&gt; c, b -&gt; c, ...} 不是排列。
因为 a 和 b 映射到同一个字母。</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 50</code></li>
	<li><code>1 &lt;= pattern.length = words[i].length&nbsp;&lt;= 20</code></li>
</ul>
</div>

## 思路
遍历pattern，判断同构字符串：
1. 如果该字母的映射是默认值，且当前目标值还未被映射，则将映射值置为当前目标值ab->cd；
2. 如果当前字母的映射值是默认值，但是当前目标值已经被映射过，则不是同构字符串ab->cc；
3. 如果该字母的映射不是默认值，且当前目标值与映射值不一致，则不是同构字符串abb->cde

## 代码
```c
#define WORD_LENGTH 21
#define ALPHA_NUMS 27
#define ALPHA_DEFAULT 30

bool PatternMatch(char *word, char *pattern)
{
    int count[ALPHA_NUMS] = {0};
    int offset[ALPHA_NUMS];
    for (int i = 0; i < ALPHA_NUMS; i++) {
        offset[i] = ALPHA_DEFAULT;
    }
    for (int i = 0; i < strlen(word); i++) {
        int offWord = word[i] - 'a';
        int offPattern = pattern[i] - 'a';
        if (offset[offPattern] == ALPHA_DEFAULT && count[offWord] == 0) {
            offset[offPattern] = offWord;
            count[offWord] = 1;
        } else if (offset[offPattern] != offWord) {
            return false; // 如果同一字母映射既不等于默认值，又不等于历史值，则表明有两个映射
        }
    }
    return true;
}
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
char ** findAndReplacePattern(char ** words, int wordsSize, char * pattern, int* returnSize){
    char **res = (char **)malloc(sizeof(char *) * wordsSize);
    for (int i = 0; i < wordsSize; i++) {
        res[i] = (char *)malloc(sizeof(char) * WORD_LENGTH);
    }
    int count = 0;

    for (int i = 0; i < wordsSize; i++) {
        if (PatternMatch(words[i], pattern)) {
            strcpy(res[count], words[i]);
            // printf("res = %s, word = %s, pattern = %s\n", res[count], words[i], pattern);
            count++;
        }
    }
    *returnSize = count;
    return res;
}
```
