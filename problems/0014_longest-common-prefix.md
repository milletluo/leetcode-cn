## [最长公共前缀(简单)](https://leetcode-cn.com/problems/longest-common-prefix/)
<p>编写一个函数来查找字符串数组中的最长公共前缀。</p>

<p>如果不存在公共前缀，返回空字符串&nbsp;<code>""</code>。</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入: </strong>["flower","flow","flight"]
<strong>输出:</strong> "fl"
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入: </strong>["dog","racecar","car"]
<strong>输出:</strong> ""
<strong>解释:</strong> 输入不存在公共前缀。
</pre>

<p><strong>说明:</strong></p>

<p>所有输入只包含小写字母&nbsp;<code>a-z</code>&nbsp;。</p>

## 思路
最长的公共前缀最长也只可能是最短的字符串  
取出最短的字符串，一次遍历最短字串的每一位，如果不是所有的字符串都与该位相等，则退出

## 代码
```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty())
            return "";
        int minLen=strs[0].length();
        int idxMin=0;
        int i;
        string out;
        for(i=0;i<strs.size();i++){
            if(minLen>strs[i].length()){
                idxMin=i;
                minLen=strs[i].length();
            }
        }
        for(int j=0;j<minLen;j++){
            for(i=0;i<strs.size();i++){
                //其实可以不用先找出最短字符串，就当第一个字符串为公共前缀，不过要在下方的出口处判断越界
                if(strs[idxMin][j]!=strs[i][j]){
                    break;
                }
            }
            if(i==strs.size()){
                out+=strs[idxMin][j];
            } else {
                break;
            }
        }
        return out;
    }
};
```
## 其他思路
[水平扫描法、分治、二分查找等](https://leetcode-cn.com/problems/longest-common-prefix/solution/zui-chang-gong-gong-qian-zhui-by-leetcode/)