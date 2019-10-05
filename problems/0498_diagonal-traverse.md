## [题目描述(中等)](https://leetcode-cn.com/problems/diagonal-traverse/)
<p>给定一个含有 M x N 个元素的矩阵（M 行，N 列），请以对角线遍历的顺序返回这个矩阵中的所有元素，对角线遍历如下图所示。</p>

<p>&nbsp;</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong>
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

<strong>输出:</strong>  [1,2,4,7,5,3,6,8,9]

<strong>解释:</strong>
<img style="width: 220px;" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/diagonal_traverse.png">
</pre>

<p>&nbsp;</p>

<p><strong>说明:</strong></p>

<ol>
	<li>给定矩阵中的元素总数不会超过 100000 。</li>
</ol>

## 思路
看图找规律，偶数层时向上遍历，奇数层，向下遍历；每一层的行数+列数=层数  
向上遍历时，常规情况行--，列++；边界时特殊处理  
向下遍历时，常规情况列--，行++；边界时特殊处理

## 代码
```c++
class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& matrix) {
        if(matrix.empty()){
            return vector<int>(0);
        }
        int i;
        int M=matrix.size();
        int N=matrix[0].size();
        vector<int> out(M*N);
        int L=M+N-1;//总层数=行数+列数-1
        int row=0;
        int col=0;
        int idx=0;
        for(i=0;i<L;i++){
            //cout<<"i"<<i<<endl;
            //偶数层时为向上遍历
            if((i&1) ==0){
                while(1){
                    //cout<<"row"<<row<<"col"<<col<<endl;
                    //从上向下转向时调整位置，要先判断列，因为如果列越界，调整动作大些
                    if(col>=N){
                        row+=2;
                        col--;
                        break;
                    } else if(row<0){
                        row++;
                        break;
                    } else{
                        out[idx++]=matrix[row][col];
                        row--;
                        col++;
                    }
                }
            } else {
                while(1){
                    //cout<<"row"<<row<<"col"<<col<<endl;
                    //从下向上转向时调整位置，要先判断行，因为如果行越界，调整动作大些
                    if (row>=M){
                        col+=2;
                        row--;
                        break;
                    } else if(col<0){
                        col++;
                        break;
                    } else{
                        out[idx++]=matrix[row][col];
                        row++;
                        col--;
                    }
                }
            }
        }
        return out;
    }
};
```
