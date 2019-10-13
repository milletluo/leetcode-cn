## [题目描述(简单)](https://leetcode-cn.com/problems/move-zeroes/)
<div class="notranslate"><p>给定一个数组 <code>nums</code>，编写一个函数将所有 <code>0</code> 移动到数组的末尾，同时保持非零元素的相对顺序。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> <code>[0,1,0,3,12]</code>
<strong>输出:</strong> <code>[1,3,12,0,0]</code></pre>

<p><strong>说明</strong>:</p>

<ol>
	<li>必须在原数组上操作，不能拷贝额外的数组。</li>
	<li>尽量减少操作次数。</li>
</ol>
</div>

## 思路
1. 冒泡，将0沉底
2. 从前往后将不等于0的依次排列，后面没排满的补零

## 代码
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int len = nums.size();
        int j = 0;
        for(int i = 0; i < len; i++) {
            if(nums[i] != 0){
                nums[j++] = nums[i];
            }
        }
        while(j < len){
            nums[j++] = 0;
        }
    }
};
```
## 其他思路
直接将快、慢指针交换
1. 慢指针（lastnonzerofoundat）之前的所有元素都是非零的。
2. 当前指针和慢速指针之间的所有元素都是零。

## 代码
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for (int lastNonZeroFoundAt = 0, cur = 0; cur < nums.size(); cur++) {
            if (nums[cur] != 0) {
                swap(nums[lastNonZeroFoundAt++], nums[cur]);
            }
        }
    }
};
```