## [螺旋矩阵III(中等))](https://leetcode-cn.com/problems/spiral-matrix-iii/)
<p>在&nbsp;<code>R</code>&nbsp;行&nbsp;<code>C</code>&nbsp;列的矩阵上，我们从&nbsp;<code>(r0, c0)</code>&nbsp;面朝东面开始</p>

<p>这里，网格的西北角位于第一行第一列，网格的东南角位于最后一行最后一列。</p>

<p>现在，我们以顺时针按螺旋状行走，访问此网格中的每个位置。</p>

<p>每当我们移动到网格的边界之外时，我们会继续在网格之外行走（但稍后可能会返回到网格边界）。</p>

<p>最终，我们到过网格的所有&nbsp;<code>R * C</code>&nbsp;个空间。</p>

<p>按照访问顺序返回表示网格位置的坐标列表。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>R = 1, C = 4, r0 = 0, c0 = 0
<strong>输出：</strong>[[0,0],[0,1],[0,2],[0,3]]

<img style="height: 99px; width: 174px;" src="https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/08/24/example_1.png" alt="">
</pre>

<p>&nbsp;</p>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>R = 5, C = 6, r0 = 1, c0 = 4
<strong>输出：</strong>[[1,4],[1,5],[2,5],[2,4],[2,3],[1,3],[0,3],[0,4],[0,5],[3,5],[3,4],[3,3],[3,2],[2,2],[1,2],[0,2],[4,5],[4,4],[4,3],[4,2],[4,1],[3,1],[2,1],[1,1],[0,1],[4,0],[3,0],[2,0],[1,0],[0,0]]

<img style="height: 142px; width: 202px;" src="https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/08/24/example_2.png" alt="">
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>1 &lt;= R &lt;= 100</code></li>
	<li><code>1 &lt;= C &lt;= 100</code></li>
	<li><code>0 &lt;= r0 &lt; R</code></li>
	<li><code>0 &lt;= c0 &lt; C</code></li>
</ol>

## 思路
每过两个方向，步长就+1，总共走的合法步数是R*C，都走完了就返回结果。

## 代码
```c++
class Solution {
public:
    vector<vector<int>> spiralMatrixIII(int R, int C, int r0, int c0) {
        int count=R*C;
        vector<vector<int>> matrix(count);
        for(int i=0;i<count;i++) {
            matrix[i].resize(2);
        }
        int step=1;
        int stepR=0,stepC=1;
        int arrow=0;
        int i=1;
        matrix[0][0]=r0;
        matrix[0][1]=c0;
        while(i<count){
            for(int j=0;j<step;j++){
                r0+=stepR;
                c0+=stepC;
                //在矩阵范围内才处理
                if(r0>=0 && r0<R && c0>=0 && c0<C){
                    matrix[i][0]=r0;
                    matrix[i][1]=c0;
                    i++;
                }
            }
            //每过两个方向步长+1
            arrow++;
            if(arrow==2){
                arrow=0;
                step++;
            }
            //每换一个方向倒换一次步幅
            //(0,1)=>(1,-0)=>(-0,-1)=>(-1,0)
            swap(stepR,stepC);
            stepC=-stepC;
        }
        return matrix;
    }
};
```
## 代码-类似状态机
```c++
class Solution {
public:
    vector<vector<int>> spiralMatrixIII(int R, int C, int r0, int c0) {
        vector<vector<int>> res;
        
        int count = 1, time = 2;
        int east = 1, south = 0, western = 0, north = 0 ;
        int sum = 0;
        while( sum < R * C){
            while( time--){
                int temp = count;
                while( temp--){
                    if( r0 > -1 && r0 < R && c0 > -1 && c0 < C)
                        res.push_back( {r0, c0}), sum++;

                    if( east )
                        r0 = r0, c0 = c0 + 1;    
                    else if( south )
                        r0 = r0 +1, c0 = c0;
                    else if( western )
                        r0 = r0, c0 = c0 - 1;
                    else if( north )
                        r0 = r0 - 1, c0 = c0;
                }
                
                if( east)
                    east = 0, south = 1;
                else if( south)
                    south = 0, western = 1;
                else if( western)
                    western = 0, north = 1;
                else if( north)
                    north = 0, east = 1;
            }
            time = 2, count++;
        }
        return res;
    }
};
```