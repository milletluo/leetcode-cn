## [无重复字符的最长子串(中等)](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)
<div class="notranslate"><p>给定一个字符串，请你找出其中不含有重复字符的&nbsp;<strong>最长子串&nbsp;</strong>的长度。</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入: </strong>"abcabcbb"
<strong>输出: </strong>3 
<strong>解释:</strong> 因为无重复字符的最长子串是 <code>"abc"，所以其</code>长度为 3。
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入: </strong>"bbbbb"
<strong>输出: </strong>1
<strong>解释: </strong>因为无重复字符的最长子串是 <code>"b"</code>，所以其长度为 1。
</pre>

<p><strong>示例 3:</strong></p>

<pre><strong>输入: </strong>"pwwkew"
<strong>输出: </strong>3
<strong>解释: </strong>因为无重复字符的最长子串是&nbsp;<code>"wke"</code>，所以其长度为 3。
&nbsp;    请注意，你的答案必须是 <strong>子串 </strong>的长度，<code>"pwke"</code>&nbsp;是一个<em>子序列，</em>不是子串。
</pre>
</div>

## 思路
滑窗法，持续扩充右边界，如果右边界值有重复，则截取重复点到右边界为新子串，比较新子串和旧子串长度，取较大值

## 代码
```c
#define MAX(a, b) (((a) > (b)) ? (a) : (b))

int lengthOfLongestSubstring(char * s){
    int res = 0;
    int begin = 0;
    int end;
    if (s == NULL) {
        return 0;
    }
    int len = strlen(s);
    // 持续扩充右边界
    for (end = 0; end < len; end++) {
        // 如果当前检查的右边界已经出现
        for (int i = begin; i < end; i++) {
            if (s[i] == s[end]) {
                begin = i + 1; // 更新左窗口边界
                break;
            }
        }
        res = MAX(res, end - begin + 1); // 更新左边界后的长度不一定是最大的，只保存较大的
    }
    return res;
}
```
