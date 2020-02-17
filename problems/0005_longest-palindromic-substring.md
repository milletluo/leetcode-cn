## [最长回文子串(中等)](https://leetcode-cn.com/problems/longest-palindromic-substring/)
<div class="notranslate"><p>给定一个字符串 <code>s</code>，找到 <code>s</code> 中最长的回文子串。你可以假设&nbsp;<code>s</code> 的最大长度为 1000。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> "babad"
<strong>输出:</strong> "bab"
<strong>注意:</strong> "aba" 也是一个有效答案。
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> "cbbd"
<strong>输出:</strong> "bb"
</pre>
<div class="notranslate"><p>给定一个字符串 <code>s</code>，找到 <code>s</code> 中最长的回文子串。你可以假设&nbsp;<code>s</code> 的最大长度为 1000。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> "babad"
<strong>输出:</strong> "bab"
<strong>注意:</strong> "aba" 也是一个有效答案。
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> "cbbd"
<strong>输出:</strong> "bb"
</pre>
</div></div>

## 思路
回文子串的特点：  
1.长度为奇数的，以某个字符为中心，往左右扩散，左右均相等；  
2.长度为偶数的，以某个字符间隙为中心，往左右扩散，左右均相等。
遍历所有字符串

## 代码
```java
class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        if (len == 0) {
            return s;
        }
        int maxLen = 1;
        int left = 0;
        int right = 0;
        for (int i = 0; i < len; i++) {
            // 遍历所有奇数长的字符串
            int l = i - 1;
            int r = i + 1;
            while (l >= 0 && r < len && s.charAt(l) == s.charAt(r)) {
                if (maxLen < r - l + 1) {
                    maxLen = r - l + 1;
                    left = l;
                    right = r;
                }
                l--;
                r++;
            }

            // 遍历所有偶数长的字符串
            l = i;
            r = i + 1;
            while (l >= 0 && r < len && s.charAt(l) == s.charAt(r)) {
                if (maxLen < r - l + 1) {
                    maxLen = r - l + 1;
                    left = l;
                    right = r;
                }
                l--;
                r++;
            }
        }
        return s.substring(left, right + 1);
    }
}
```
