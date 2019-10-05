## [题目描述(简单)](https://leetcode-cn.com/problems/largest-number-at-least-twice-of-others/)
<p>在一个给定的数组<code>nums</code>中，总是存在一个最大元素 。</p>

<p>查找数组中的最大元素是否至少是数组中每个其他数字的两倍。</p>

<p>如果是，则返回最大元素的索引，否则返回-1。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> nums = [3, 6, 1, 0]
<strong>输出:</strong> 1
<strong>解释:</strong> 6是最大的整数, 对于数组中的其他整数,
6大于数组中其他元素的两倍。6的索引是1, 所以我们返回1.
</pre>

<p>&nbsp;</p>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> nums = [1, 2, 3, 4]
<strong>输出:</strong> -1
<strong>解释:</strong> 4没有超过3的两倍大, 所以我们返回 -1.
</pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ol>
	<li><code>nums</code>&nbsp;的长度范围在<code>[1, 50]</code>.</li>
	<li>每个&nbsp;<code>nums[i]</code>&nbsp;的整数范围在&nbsp;<code>[0, 100]</code>.</li>
</ol>

## 思路
直观解法，第一次遍历找出最大值，第二次遍历判断其他值的2倍小于最大值

## 代码
```c++
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
        int max=0;
        int idx=0;
        int i;
        
        for(i=0;i<nums.size();i++){
            if(nums[i]>max){
                max=nums[i];
                idx=i;
            }
        }
        for(i=0;i<nums.size();i++){
            if(2*nums[i]>max && i!=idx){
                return -1;
            }
        }
        return idx;
    }
};
```
## 其他思路
只需要找到第二大的元素，将它的两倍的值与最大值进行比较，就能证明最大值是否大于所有元素两倍。只需要一次循环

## 代码
```c++
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
        int max=0;
        int maxSecond=0;
        int idx=0;
        int i;
        
        for(i=0;i<nums.size();i++){
            if(nums[i]>max){
                maxSecond = max;
                max=nums[i];
                idx=i;
            } else if(nums[i]>maxSecond){
                maxSecond = nums[i];
            }
        }
        if(2*maxSecond>max){
            return -1;
        }
        return idx;
    }
};
```