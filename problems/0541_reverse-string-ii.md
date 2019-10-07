## [题目描述(简单)](https://leetcode-cn.com/problems/reverse-string-ii/)
<p>给定一个字符串和一个整数 k，你需要对从字符串开头算起的每个 2k 个字符的前k个字符进行反转。如果剩余少于 k 个字符，则将剩余的所有全部反转。如果有小于 2k 但大于或等于 k 个字符，则反转前 k 个字符，并将剩余的字符保持原样。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> s = "abcdefg", k = 2
<strong>输出:</strong> "bacdfeg"
</pre>

<p><strong>要求:</strong></p>

<ol>
	<li>该字符串只包含小写的英文字母。</li>
	<li>给定字符串的长度和 k 在[1, 10000]范围内。</li>
</ol>

## 思路
退出条件：没有剩余要处理的字符  
定位要交换部分的首尾位置  
双指针，分别从首和尾开始遍历，交换首尾  
更新要交换部分的首尾位置，更新剩余要处理的字符个数

## 代码
```c++
class Solution {
public:
    string reverseStr(string s, int k) {
        int len=s.length();
        int begin=0;
        int end;
        int remain=len;
        while(remain!=0){
            if(remain>=2*k){
                end=begin+k-1;
                remain-=2*k;
            }else if(remain<2*k && remain>=k){
                end=begin+k-1;
                remain=0;
            }else{
                end=len-1;
                remain=0;
            }
            while(begin<end){
                swap(s[begin],s[end]);
                begin++;
                end--;
            }
            begin=len-remain;
        }
        return s;
    }
};
```
## 其他思路
我们直接翻转每个 2k 字符块。

每个块开始于 2k 的倍数，也就是 0, 2k, 4k, 6k, ...。需要注意的一件是：如果没有足够的字符，我们并不需要翻转这个块。

为了翻转从 i 到 j 的字符块，我们可以交换位于 i++ 和 j-- 的字符。

## 代码
```c++
class Solution {
public:
    string reverseStr(string s, int k) {
        int len=s.length();
        for(int i=0;i<len;i+=2*k){
            if(len-1-i>=k)
                reverseString(s,i,i+k-1);
            else
                reverseString(s,i,len-1);
        }
        return s;
    }
private:
    void reverseString(string &s, int i, int j) {
        while(i<j){
            swap(s[i],s[j]);
            i++;
            j--;
        }
    }
};
```
## 代码
```c++
class Solution {
public:
    string reverseStr(string s, int k) {
	for (string::iterator it = s.begin(); it < s.end(); it += 2 * k)
		if (it + k <= s.end()) reverse(it, it + k);
		else reverse(it, s.end());
	return s;
    }
};
```