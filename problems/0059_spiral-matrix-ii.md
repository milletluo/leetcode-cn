## [题目描述(中等))](https://leetcode-cn.com/problems/spiral-matrix-ii/)
<p>给定一个正整数&nbsp;<em>n</em>，生成一个包含 1 到&nbsp;<em>n</em><sup>2</sup>&nbsp;所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> 3
<strong>输出:</strong>
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]</pre>

## 思路
借用题54的螺旋方式

## 代码
```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        if(n==0)
            return vector<vector<int>>(0);
        vector<vector<int>> matrix(n);
        for(int i=0;i<n;i++) {
            matrix[i].resize(n);
        }
        int value=1;
        int u = 0; //赋值上下左右边界
        int d = matrix.size() - 1;
        int l = 0;
        int r = matrix[0].size() - 1;
        int i;
        while(true)
        {
            for(i = l; i <= r; ++i) matrix[u][i]=value++; //向右移动直到最右
            if(++ u > d) break; //重新设定上边界，若上边界大于下边界，则遍历遍历完成，下同
            for(i = u; i <= d; ++i) matrix[i][r]=value++; //向下
            if(-- r < l) break; //重新设定有边界
            for(i = r; i >= l; --i) matrix[d][i]=value++; //向左
            if(-- d < u) break; //重新设定下边界
            for(i = d; i >= u; --i) matrix[i][l]=value++; //向上
            if(++ l > r) break; //重新设定左边界
        }
        return matrix;
    }
};
```
