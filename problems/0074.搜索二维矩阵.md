## [搜索二维矩阵(中等)](https://leetcode-cn.com/problems/search-a-2d-matrix/)
<div class="notranslate"><p>编写一个高效的算法来判断&nbsp;<em>m</em> x <em>n</em>&nbsp;矩阵中，是否存在一个目标值。该矩阵具有如下特性：</p>

<ul>
	<li>每行中的整数从左到右按升序排列。</li>
	<li>每行的第一个整数大于前一行的最后一个整数。</li>
</ul>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入:</strong>
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
<strong>输出:</strong> true
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong>
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
<strong>输出:</strong> false</pre>
</div>

## 思路
可以看为有序的一维数组，采用二分法  
模板：
```
while(low <= high) {
    // 如果写成mid = (low+high)/2是有问题,如果low和high比较大,两者的和可能会溢出
    int mid = low +((high - low)>> 1);
    if(A[mid] == value)
        return mid;
    else if (A[mid] < value)
        low = mid +1;
    else
        high = mid -1;
}
```

## 代码
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = matrix.length;
        if (row == 0 || matrix[0].length == 0) {
            return false;
        }
        int col = matrix[0].length;
        int left = 0;
        int right = row * col - 1;
        int mid = 0;
        while (left <= right) {
            mid = left + (right - left) / 2;
            int temp = matrix[mid / col][mid % col];
            if (temp > target) {
                right = mid - 1;
            } else if (temp < target) {
                left = mid + 1;
            } else {
                return true;
            }
        }
        return false;
    }
}
```
## 其他思路
利用矩阵升序的特性，从右上角往左下角比较。  
如果当前值比目标值小，增行；如果当前值比目标值大，减列

## 代码
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length == 0)
            return false;
        int row = 0, col = matrix[0].length-1;
        while(row < matrix.length && col >= 0){
            if(matrix[row][col] < target)
                row++;
            else if(matrix[row][col] > target)
                col--;
            else
                return true;
        }
        return false;
    }
}
```