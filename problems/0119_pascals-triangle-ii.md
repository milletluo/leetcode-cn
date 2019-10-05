## [题目描述(简单)](https://leetcode-cn.com/problems/pascals-triangle-ii/)
<p>给定一个非负索引&nbsp;<em>k</em>，其中 <em>k</em>&nbsp;≤&nbsp;33，返回杨辉三角的第 <em>k </em>行。</p>

<p><img src="https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif" alt=""></p>

<p><small>在杨辉三角中，每个数是它左上方和右上方的数的和。</small></p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> 3
<strong>输出:</strong> [1,3,3,1]
</pre>

<p><strong>进阶：</strong></p>

<p>你可以优化你的算法到 <em>O</em>(<em>k</em>) 空间复杂度吗？</p>

## 思路
倒着计算每行数据，更新完j的信息后，虽然把j之前的信息覆盖掉了。  
但是下一次我们更新的是j - 1，需要的是j - 1和j - 2 的信息，j信息覆盖就不会造成影响了。
```
{1},
{1,1},
{1,2,1},
{1,3,3,1},
{1,4,6,4,1},
```

## 代码
```c++
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> out(rowIndex+1,1);
        for(int i=0;i<=rowIndex;i++){
            for(int j=i-1;j>0;j--){
                out[j]=out[j]+out[j-1];
            }
        }
        return out;
    }
};
```
