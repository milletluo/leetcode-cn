## [题目描述(简单)](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)
<p>给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre>输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc"<strong><strong><strong>&nbsp;</strong></strong></strong>
</pre>

<p><strong><strong><strong><strong>注意：</strong></strong></strong></strong>在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。</p>

## 思路
找到空格时翻转一次，同时更新坐标  

## 代码
```c++
class Solution {
public:
    string reverseWords(string s) {
        int begin=0;
        for(int i=0;i<s.length();i++){
            if(s[i]==' '){
                reverse(s.begin()+begin, s.begin()+i);
                begin=i+1;
            }
        }
        reverse(s.begin()+begin, s.end());
        return s;
    }
};
```