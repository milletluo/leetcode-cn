## [题目描述(简单)](https://leetcode-cn.com/problems/pascals-triangle/)
<p>给定一个非负整数&nbsp;<em>numRows，</em>生成杨辉三角的前&nbsp;<em>numRows&nbsp;</em>行。</p>

<p><img src="https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif" alt=""></p>

<p><small>在杨辉三角中，每个数是它左上方和右上方的数的和。</small></p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> 5
<strong>输出:</strong>
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]</pre>

## 思路
初始化数组后，每一行的首位置1，中间的用上一行的左右值相加

## 代码
```c++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> out(numRows);
        for(int i=0;i<numRows;i++){
            out[i].resize(i+1);
        }
        for(int i=0;i<numRows;i++){
            for(int j=0;j<i+1;j++){
                if(j==0 || j==i){
                    out[i][j]=1;
                } else {
                    out[i][j]=out[i-1][j-1]+out[i-1][j];
                }
            }
        }
        return out;
    }
};
```
## 代码
```c++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ans(numRows);
        if(numRows == 0)    return ans; //若numRows为空，返回空数组
        for(int i = 0; i < numRows; ++ i ) //给数组一个个赋值
        {
            for(int j = 0; j <= i; ++ j)
            {
                if(j == 0 || j == i) //若是左右两边的边界，赋值为1
                    ans[i].push_back(1);
                else
                    ans[i].push_back(ans[i-1][j-1] + ans[i-1][j]); //否则赋值为该位置左上与右上的和
            }
        }
        return ans;
    }
};
```