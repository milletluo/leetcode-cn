## [回文子串(中等)](https://leetcode-cn.com/problems/palindromic-substrings/)
<div class="notranslate"><p>给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。</p>

<p>具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被计为是不同的子串。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> "abc"
<strong>输出:</strong> 3
<strong>解释:</strong> 三个回文子串: "a", "b", "c".
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> "aaa"
<strong>输出:</strong> 6
<strong>说明:</strong> 6个回文子串: "a", "a", "a", "aa", "aa", "aaa".
</pre>

<p><strong>注意:</strong></p>

<ol>
	<li>输入的字符串长度不会超过1000。</li>
</ol>
</div>

## 思路
动态规划：dp[i][j]表示从i起到j止的字符串是否为回文子串  
遍历所有长度的子串，用短的快速判断长的

## 代码
```java
class Solution {
    public int countSubstrings(String s) {
        int len = s.length();
        // dp[i][j]表示从i起到j止的字符串是否为回文子串
        boolean[][] dp = new boolean[len][len];
        int res = 0;

        // 所有单个字符都是回文子串
        for (int i = 0; i < len; i++) {
            dp[i][i] = true;
            res++;
        }

        // 相邻两个相同字符也是回文子串
        for (int i = 0; i < len - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                res++;
            }
        }

        // 通过较短的字符串判断较长的字符串是否是回文子串（在两端加相同的字符则特性保持不变）
        for (int k = 3; k <= len; k++) {
            for (int i = 0; i + k - 1 < len; i++) {
                int j = i + k - 1;
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1];
                    if (dp[i][j] == true) {
                        res++;
                    }
                }
            }
        }
        return res;
    }
}
```
