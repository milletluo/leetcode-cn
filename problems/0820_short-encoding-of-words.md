## [题目描述(中等)](https://leetcode-cn.com/problems/short-encoding-of-words/)
<div class="notranslate"><p>给定一个单词列表，我们将这个列表编码成一个索引字符串&nbsp;<code>S</code>&nbsp;与一个索引列表 <code>A</code>。</p>

<p>例如，如果这个列表是 <code>["time", "me", "bell"]</code>，我们就可以将其表示为 <code>S = "time#bell#"</code> 和 <code>indexes = [0, 2, 5]</code>。</p>

<p>对于每一个索引，我们可以通过从字符串 <code>S</code>&nbsp;中索引的位置开始读取字符串，直到 "#" 结束，来恢复我们之前的单词列表。</p>

<p>那么成功对给定单词列表进行编码的最小字符串长度是多少呢？</p>

<p>&nbsp;</p>

<p><strong>示例：</strong></p>

<pre><strong>输入:</strong> words = <code>["time", "me", "bell"]</code>
<strong>输出:</strong> 10
<strong>说明:</strong> S = <code>"time#bell#" ， indexes = [0, 2, 5</code>] 。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>1 &lt;= words.length&nbsp;&lt;= 2000</code></li>
	<li><code>1 &lt;=&nbsp;words[i].length&nbsp;&lt;= 7</code></li>
	<li>每个单词都是小写字母 。</li>
</ol>
</div>

## 思路
1. 将长串排前面，先处理
2. 逐个由长到短遍历，如果在结果中找不到以#结尾匹配的，加入索引字符串

## 代码
```c
int cmp(const void *aa, const void *bb)
{
    char *a = *(char**)aa;
    char *b = *(char**)bb;
    return strlen(b) - strlen(a);
}

int minimumLengthEncoding(char ** words, int wordsSize)
{
    char curString[10] = {0};
    char res[16000] = {0};
    // 将长串排前面，先处理
    qsort(words, wordsSize, sizeof(char *), cmp);
    for (int i = 0; i < wordsSize; i++) {
        memset(curString, 0, 10);
        strcat(curString, words[i]);
        strcat(curString, "#");
        // 如果能找到以#结尾的子串则跳过，否则增加到S尾部
        if (strstr(res, curString) == NULL) {
            strcat(res, curString);
        }
        // printf("cur = %s, word = %s\n", curString, words[i]);
    }
    // printf("res = %s, len = %d\n", res, strlen(res));
    return strlen(res);
}
```
