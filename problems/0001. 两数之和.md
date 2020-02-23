## [两数之和(简单)](https://leetcode-cn.com/problems/two-sum/)
<p>给定一个整数数组 <code>nums</code>&nbsp;和一个目标值 <code>target</code>，请你在该数组中找出和为目标值的那&nbsp;<strong>两个</strong>&nbsp;整数，并返回他们的数组下标。</p>
<p>你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。</p>
<p><strong>示例:</strong></p>
<pre>给定 nums = [2, 7, 11, 15], target = 9

因为 nums[<strong>0</strong>] + nums[<strong>1</strong>] = 2 + 7 = 9
所以返回 [<strong>0, 1</strong>]
</pre>

## 思路
暴力遍历，查找不到时返回0

## 代码
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int i,j;
        vector<int> out(2);
        vector<int> err;
        for(i=0;i<nums.size()-1;i++){
            for(j=i+1;j<nums.size();j++){
                if(nums[i]+nums[j]==target){
                    out[0]=i;
                    out[1]=j;
                    return out;
                }
            }
        }
        return err;
    }
};
```

## 其他思路
思路：采取一边插入哈希表一边寻找一边在已经插入的哈希表中寻找的方式，每次都拿着即将插入哈希表的数字然后在哈希表中找是否存在剩下的那个函数。有人可能会问，在循环里面查找的话时间复杂度不就变高了嘛，但是哈希表查找时间可以说是o(1)是常数（避免冲突的算法采用链地址可能不为o(1)，但一般不用链地址来避免冲突），所以总的时间复杂度就为o(n)，哈希表就是一种用空间换取时间的算法。

## 代码
```
class Solution {
public:  
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> res;
        unordered_map<int, int> hash;//由于unorder_map速度要比map快所以选择无序哈希表  
        for(int i=0; i < nums.size();++i){
            int another = target - nums[i];
            if(hash.count(another)){  
                res = vector<int>({hash[another], i});
                return res;
            }
            hash[nums[i]] = i;
        }
        return res;
    }
};

```

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    res[0] = i;
                    res[1] = j;
                    return res;
                }
            }
        }
        return res;
    }
}
```