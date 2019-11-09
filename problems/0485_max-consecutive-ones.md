## [最大连续1的个数(简单)](https://leetcode-cn.com/problems/max-consecutive-ones/)
<p>给定一个二进制数组， 计算其中最大连续1的个数。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> [1,1,0,1,1,1]
<strong>输出:</strong> 3
<strong>解释:</strong> 开头的两位和最后的三位都是连续1，所以最大连续1的个数是 3.
</pre>

<p><strong>注意：</strong></p>

<ul>
	<li>输入的数组只包含&nbsp;<code>0</code> 和<code>1</code>。</li>
	<li>输入数组的长度是正整数，且不超过 10,000。</li>
</ul>

## 思路
遍历,如果是1，临时记录++，如果变为0，取临时记录和历史记录较大值，同时更新临时记录为0

## 代码
```c++
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int count=0,countTemp=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==1){
                countTemp++;
            }else{
                count=max(count,countTemp);
                countTemp=0;
            }
        }
        return max(count,countTemp);
    }
};
```
## 其他思路
快慢双指针，快指针查找1并记录临时长度，查到0时更新慢指针，更新最大长度

## 代码
```c++
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int count=0,countTemp=0;
        int fast=0,slow=0;
        while(slow<nums.size()){
            fast=slow;
            countTemp=0;
            while(fast<nums.size() && nums[fast++]==1)
                countTemp++;
            count=max(count,countTemp);
            slow=fast;
        }
        return count;
    }
};
```