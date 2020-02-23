## [第k个排列(中等)](https://leetcode-cn.com/problems/permutation-sequence/)
<div class="notranslate"><p>给出集合&nbsp;<code>[1,2,3,…,<em>n</em>]</code>，其所有元素共有&nbsp;<em>n</em>! 种排列。</p>

<p>按大小顺序列出所有排列情况，并一一标记，当&nbsp;<em>n </em>= 3 时, 所有排列如下：</p>

<ol>
	<li><code>"123"</code></li>
	<li><code>"132"</code></li>
	<li><code>"213"</code></li>
	<li><code>"231"</code></li>
	<li><code>"312"</code></li>
	<li><code>"321"</code></li>
</ol>

<p>给定&nbsp;<em>n</em> 和&nbsp;<em>k</em>，返回第&nbsp;<em>k</em>&nbsp;个排列。</p>

<p><strong>说明：</strong></p>

<ul>
	<li>给定<em> n</em>&nbsp;的范围是 [1, 9]。</li>
	<li>给定 <em>k&nbsp;</em>的范围是[1, &nbsp;<em>n</em>!]。</li>
</ul>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入:</strong> n = 3, k = 3
<strong>输出:</strong> "213"
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> n = 4, k = 9
<strong>输出:</strong> "2314"
</pre>
</div>

## [思路](https://www.bilibili.com/video/av83725059?from=search&seid=17537325435983430772)
列出一组数据找规律，
从第0位开始，如果首位固定，则后面排列方式有(n-1)!种；

如果k<=(n-1)!，则首位可定；否则继续下移一组（每个首位组间隔(n-1)!个）

## 代码
```java
class Solution {
    public String getPermutation(int n, int k) {
        int[] jiecheng = new int[n + 1];
        jiecheng[0] = 1;
        jiecheng[1] = 1;
        // 算出每位数的阶乘
        for (int i = 2; i <= n; i++) {
            jiecheng[i] = i * jiecheng[i - 1];
        }
        // 准备数据池
        List<Integer> numbers = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            numbers.add(i);
        }

        StringBuilder res = new StringBuilder();
        // 从最高位（第0位）开始遍历
        for (int  i = 0; i < n; i++) {
            // 从最小的数开始遍历
            for (int j = 0; j < numbers.size(); j++) {
                // 如果k在(n-1)!个数以内，则取当前遍历到的数，并移出数据池
                if (k <= jiecheng[n - 1 - i]) {
                    res.append(numbers.get(j));
                    numbers.remove(j);
                    break;
                } else { // 如果k大于(n-1)!，则k减去前面的(n-1)!个数
                    k = k - jiecheng[n - 1 - i];
                }
            }
        }
        return res.toString();
    }
}
```
