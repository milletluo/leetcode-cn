## [剑指 Offer 38. 字符串的排列(中等)](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)
<div class="notranslate"><p>输入一个字符串，打印出该字符串中字符的所有排列。</p>

<p>&nbsp;</p>

<p>你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。</p>

<p>&nbsp;</p>

<p><strong>示例:</strong></p>

<pre><strong>输入：</strong>s = "abc"
<strong>输出：[</strong>"abc","acb","bac","bca","cab","cba"<strong>]</strong>
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>1 &lt;= s 的长度 &lt;= 8</code></p>
</div>

## 思路
回溯模板
* 使用sort函数对字符串排序，使重复的字符相邻，
* 使用visit数组记录遍历决策树时每个节点的状态，
* 节点未遍历且相邻字符不是重复字符时，
* 则将该字符加入排列字符串中，依次递归遍历。

## 代码
```java
class Solution {
    private List<String> res = new ArrayList<>();
    public String[] permutation(String s) {
        char[] chars = s.toCharArray();
        Arrays.sort(chars);
        int[] visited = new int[chars.length];
        StringBuilder sb = new StringBuilder();
        backtrack(chars, sb, visited);
        return res.toArray(new String[res.size()]);
    }
    private void backtrack(char[] chars, StringBuilder sb, int[] visited) {
        if (sb.length() == chars.length) {
            res.add(sb.toString());
            return;
        }
        for (int i = 0; i < chars.length; i++) {
            if (visited[i] == 0) {
                // 剪枝：如果这个字符和之前的字符一样，并且之前的字符还未使用过（说明已经回溯过，由1变为0）
                if (i > 0 && chars[i] == chars[i - 1] && visited[i - 1] == 0) {
                    continue;
                }
                sb.append(chars[i]);
                visited[i] = 1;
                backtrack(chars, sb, visited);
                visited[i] = 0;
                sb.deleteCharAt(sb.length() - 1);
            }
        }
    }
}
```
