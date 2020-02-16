## [前 K 个高频元素(中等)](https://leetcode-cn.com/problems/top-k-frequent-elements/)
<div class="notranslate"><p>给定一个非空的整数数组，返回其中出现频率前&nbsp;<strong><em>k&nbsp;</em></strong>高的元素。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入: </strong>nums = [1,1,1,2,2,3], k = 2
<strong>输出: </strong>[1,2]
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入: </strong>nums = [1], k = 1
<strong>输出: </strong>[1]</pre>

<p><strong>说明：</strong></p>

<ul>
	<li>你可以假设给定的&nbsp;<em>k&nbsp;</em>总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。</li>
	<li>你的算法的时间复杂度<strong>必须</strong>优于 O(<em>n</em> log <em>n</em>) ,&nbsp;<em>n&nbsp;</em>是数组的大小。</li>
</ul>
</div>

## 思路
桶排序法，首先使用哈希表统计频率，统计完成后，创建一个数组，将频率作为数组下标，对于出现频率不同的数字集合，存入对应的数组下标。  
然后从后往前取k个。

## 代码
```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        int maxTimes = -1;
        //将每个数的频次的统计结果存入哈希表
        for(int num : nums){
            if(!map.containsKey(num)){
                map.put(num, 1);
            }else{
                map.put(num, map.get(num) + 1);
            }
            maxTimes = map.get(num) > maxTimes ? map.get(num) : maxTimes;
        }
        //需要注意的是：这里new的只是一个引用变量数组，它们初始化是指向null的
        ArrayList<Integer>[] buckets = new ArrayList[maxTimes + 1];
        //将每个数插入索引为它的频次的那个桶里
        for(int num : map.keySet()){
            int frequency = map.get(num);
            if(buckets[frequency] == null){
                buckets[frequency] = new ArrayList<>();
            }
            buckets[frequency].add(num);
        }
        //由于桶的索引的含义是数出现的频次，越在数组后面的频次就越高
        //想要求出频次最高的k个数，只需要倒着遍历桶即可
        //这里做的是将倒着遍历到的k个数放入要作为结果返回的List中
        List<Integer> result = new ArrayList<>();
        for(int i = maxTimes; i >= 0 && k > 0; i--){
            if(buckets[i] != null){
                //桶的索引的含义是数的频次，因此一个桶里可能有多个数
                for(int num : buckets[i]){
                    if(k > 0){
                        k--;
                        result.add(num);
                    }else{
                        break;
                    }
                }
            }
        }
        return result;
    }
}
```

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        if (nums == null || nums.length < k) {
            return null;
        }
        Map<Integer, Integer> calc = new HashMap<Integer, Integer>();
        for (int num : nums) {
            calc.put(num, calc.getOrDefault(num, 0) + 1);
        }
        List<Integer> res = calc.entrySet()
            .stream()
            .sorted((a, b) -> (b.getValue() - a.getValue()))
            .map(a -> a.getKey())
            .collect(Collectors.toList());
        return res.subList(0, k);
    }
}
```