## [每日温度(中等)](https://leetcode-cn.com/problems/daily-temperatures/)
<div class="notranslate"><p>根据每日 <code>气温</code> 列表，请重新生成一个列表，对应位置的输入是你需要再等待多久温度才会升高超过该日的天数。如果之后都不会升高，请在该位置用&nbsp;<code>0</code> 来代替。</p>

<p>例如，给定一个列表&nbsp;<code>temperatures = [73, 74, 75, 71, 69, 72, 76, 73]</code>，你的输出应该是&nbsp;<code>[1, 1, 4, 2, 1, 1, 0, 0]</code>。</p>

<p><strong>提示：</strong><code>气温</code> 列表长度的范围是&nbsp;<code>[1, 30000]</code>。每个气温的值的均为华氏度，都是在&nbsp;<code>[30, 100]</code>&nbsp;范围内的整数。</p>
</div>

## 思路
方法1：暴力遍历  
方法2：从后往前遍历，记录下当前温度出现的下标，对每一个当前遍历到温度，再遍历所有比他大的温度，如果出现过，则求最小下标差

## 代码
```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        int len = T.length;
        int[] res = new int[len];
        for (int i = 0; i < len; i++) {
            res[i] = 0;
            // 找到第一个比当前温度大的，序号差既所求
            for (int j = i + 1; j < len; j++) {
                if (T[i] < T[j]) {
                    res[i] = j - i;
                    break;
                }
            }
        }
        return res;
    }
}
```

```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        int len = T.length;
        int[] temper = new int[101];
        int[] res = new int[len];
        Arrays.fill(res, len);
        // 倒着遍历
        for (int i = len - 1; i >= 0; i--) {
            for (int j = T[i] + 1; j < 101; j++) {
                // 如果温度内容不为0，表示该温度之前出现过
                if (temper[j] != 0) {
                    // 遍历比当前温度大的温度，取下标最接近的差值
                    res[i] = Math.min(res[i], temper[j] - i);
                }
            }
            // 将温度的下标填充到对应温度的内容
            temper[T[i]] = i;
        }
        for (int i = 0; i < len; i++) {
            if (res[i] == len) {
                res[i] = 0;
            }
        }
        return res;
    }
}
```