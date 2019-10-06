## [题目描述(简单)](https://leetcode-cn.com/problems/template/)
<p>实现&nbsp;<a href="https://baike.baidu.com/item/strstr/811469">strStr()</a>&nbsp;函数。</p>

<p>给定一个&nbsp;haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回&nbsp; <strong>-1</strong>。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> haystack = "hello", needle = "ll"
<strong>输出:</strong> 2
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> haystack = "aaaaa", needle = "bba"
<strong>输出:</strong> -1
</pre>

<p><strong>说明:</strong></p>

<p>当&nbsp;<code>needle</code>&nbsp;是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。</p>

<p>对于本题而言，当&nbsp;<code>needle</code>&nbsp;是空字符串时我们应当返回 0 。这与C语言的&nbsp;<a href="https://baike.baidu.com/item/strstr/811469">strstr()</a>&nbsp;以及 Java的&nbsp;<a href="https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)">indexOf()</a>&nbsp;定义相符。</p>

## 思路
找到与短串首位相同的位置后，一直比较到短串结束，如果都相等则找到  
如果中间不相等，或者长串越界则退出

## 代码
```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle.length()==0)
            return 0;
        if(haystack.length()==0 || haystack.length()<needle.length())
            return -1;
        int idxH=0;
        int idxN=0;
        int lenN=needle.length();
        for(int i=0;i<haystack.length();i++){
            if(haystack[i]==needle[0]){
                idxH=i;
                for(idxN=0;idxN<needle.length();idxN++){
                    if(idxN>=haystack.length() || haystack[idxH++]!=needle[idxN])
                        break;
                }
                if(idxN==needle.length())
                    return i;
            }
        }
        return -1;
    }
};
```
## 其他思路
[KMP算法](https://leetcode-cn.com/problems/implement-strstr/solution/kmp-suan-fa-xiang-jie-by-labuladong/)