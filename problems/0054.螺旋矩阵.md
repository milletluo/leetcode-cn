## [螺旋矩阵(中等)](https://leetcode-cn.com/problems/spiral-matrix/)
<p>给定一个包含&nbsp;<em>m</em> x <em>n</em>&nbsp;个元素的矩阵（<em>m</em> 行, <em>n</em> 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入:</strong>
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
<strong>输出:</strong> [1,2,3,6,9,8,7,4,5]
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong>
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
<strong>输出:</strong> [1,2,3,4,8,12,11,10,9,5,6,7]
</pre>

## 思路
梳理出各个方向遍历时下标的变化，switch-case分别处理，注意边界处理

## 代码
```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.empty()){
            return vector<int>(0);
        }
        int i;
        int M=matrix.size();
        int N=matrix[0].size();
        vector<int> out(M*N);
        int row=0;
        int col=0;
        int arrow=0;//当前遍历方向
        int left=0;//初始化各个边界
        int right=N-1;
        int top=1;
        int bottom=M-1;
        for(i=0;i<M*N;i++){
            switch (arrow) {
                case 0:{//从左往右
                    out[i]=matrix[row][col];
                    if(col==right){ //抵达右边界
                        row++;      //往下移一位，由于i的约束，不会访问越界
                        right--;    //更新右边界
                        arrow=1;    //调整遍历方向
                    } else {        //未抵达右边界时一直往右
                        col++;
                    }
                    break;
                }
                case 1:{//从上往下
                    out[i]=matrix[row][col];
                    if(row==bottom){
                        col--;
                        bottom--;
                        arrow=2;
                    } else {
                        row++;
                    }
                    break;
                }
                case 2:{//从右往左
                    out[i]=matrix[row][col];
                    if(col==left){
                        row--;
                        left++;
                        arrow=3;
                    } else {
                        col--;
                    }
                    break;
                }
                case 3:{//从下往上
                    out[i]=matrix[row][col];
                    if(row==top){
                        col++;
                        top++;
                        arrow=0;
                    } else {
                        row--;
                    }
                    break;
                }
                default:
                    break;
            }
        }
        return out;
    }
};
```

## 其他思路
其实是同一种思路，不过写得更漂亮
1. 首先设定上下左右边界
2. 其次向右移动到最右，此时第一行因为已经使用过了，可以将其从图中删去，体现在代码中就是重新定义上边界
3. 判断若重新定义后，上下边界交错，表明螺旋矩阵遍历结束，跳出循环，返回答案
4. 若上下边界不交错，则遍历还未结束，接着向下向左向上移动，操作过程与第一，二步同理
5. 不断循环以上步骤，直到某两条边界交错，跳出循环，返回答案
## 代码
```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector <int> ans;
        if(matrix.empty()) return ans; //若数组为空，直接返回答案
        int u = 0; //赋值上下左右边界
        int d = matrix.size() - 1;
        int l = 0;
        int r = matrix[0].size() - 1;
        int i;
        while(true)
        {
            for(i = l; i <= r; ++i) ans.push_back(matrix[u][i]); //向右移动直到最右
            if(++ u > d) break; //重新设定上边界，若上边界大于下边界，则遍历遍历完成，下同
            for(i = u; i <= d; ++i) ans.push_back(matrix[i][r]); //向下
            if(-- r < l) break; //重新设定有边界
            for(i = r; i >= l; --i) ans.push_back(matrix[d][i]); //向左
            if(-- d < u) break; //重新设定下边界
            for(i = d; i >= u; --i) ans.push_back(matrix[i][l]); //向上
            if(++ l > r) break; //重新设定左边界
        }
        return ans;
    }
};
```