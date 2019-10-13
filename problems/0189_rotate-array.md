## [题目描述(简单)](https://leetcode-cn.com/problems/rotate-array/)
<div class="notranslate"><p>给定一个数组，将数组中的元素向右移动&nbsp;<em>k&nbsp;</em>个位置，其中&nbsp;<em>k&nbsp;</em>是非负数。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> <code>[1,2,3,4,5,6,7]</code> 和 <em>k</em> = 3
<strong>输出:</strong> <code>[5,6,7,1,2,3,4]</code>
<strong>解释:</strong>
向右旋转 1 步: <code>[7,1,2,3,4,5,6]</code>
向右旋转 2 步: <code>[6,7,1,2,3,4,5]
</code>向右旋转 3 步: <code>[5,6,7,1,2,3,4]</code>
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> <code>[-1,-100,3,99]</code> 和 <em>k</em> = 2
<strong>输出:</strong> [3,99,-1,-100]
<strong>解释:</strong> 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]</pre>

<p><strong>说明:</strong></p>

<ul>
	<li>尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。</li>
	<li>要求使用空间复杂度为&nbsp;O(1) 的&nbsp;<strong>原地&nbsp;</strong>算法。</li>
</ul>
</div>

## 思路
暴力法，利用vector添加和删除首尾的能力，每移动一次分别操作一次  
总是往一个方向走遇到大数组会超时，提前判断下移动方向能减少一半时间

## 代码
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int len = nums.size();
        if(len == 0){
            return;
        }
        int step = k % len;
        if(step > len/2 ){
            step = len - step;
            while(step > 0) {
                int temp = nums[0];
                nums.erase(nums.begin());
                nums.push_back(temp);
                step--;
            }
        } else {
            while(step > 0) {
                int temp = nums[len - 1];
                nums.pop_back();
                nums.insert(nums.begin(), 1, temp);
                step--;
            }
        }
    }
};
```
## 其他思路
1. 使用一个额外数组，`i`放到`(i+k)%长度`的位置，再拷贝到原数组
2. 当我们旋转数组 k 次，`k%n`个尾部元素会被移动到头部，剩下的元素会被向后移动。
先将所有元素反转。然后反转前`k`个元素，再反转后面`n-k`个元素。
```
原始数组                  : 1 2 3 4 5 6 7
反转所有数字后             : 7 6 5 4 3 2 1
反转前 k 个数字后          : 5 6 7 4 3 2 1
反转后 n-k 个数字后        : 5 6 7 1 2 3 4 --> 结果
```
## 代码
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int len = nums.size();
        if(len == 0){
            return;
        }
        int step = k % len;
        reverse(nums.begin(),nums.end());
        reverse(nums.begin(),nums.begin()+step);
        reverse(nums.begin()+step,nums.end());
    }
};
```