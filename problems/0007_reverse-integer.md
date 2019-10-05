## [题目描述(简单)](https://leetcode-cn.com/problems/reverse-integer/)
<p>给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。</p>
<p><strong>示例&nbsp;1:</strong></p>
<pre><strong>输入:</strong> 123
<strong>输出:</strong> 321
</pre>
<p><strong>&nbsp;示例 2:</strong></p>
<pre><strong>输入:</strong> -123
<strong>输出:</strong> -321
</pre>
<p><strong>示例 3:</strong></p>
<pre><strong>输入:</strong> 120
<strong>输出:</strong> 21
</pre>
<p><strong>注意:</strong></p>
<p>假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为&nbsp;[−2<sup>31</sup>,&nbsp; 2<sup>31&nbsp;</sup>− 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。</p>

## 思路
取余得到个位后*10作高位

注意越界情况特殊处理，定义为long可以直接判断反转后的int边界是否越界，但是不完全满足题目要求

溢出条件有两个，一个是大于整数最大值MAX_VALUE，另一个是小于整数最小值MIN_VALUE，设当前计算结果为ans，下一位为pop。

1. 从ans * 10 + pop > MAX_VALUE这个溢出条件来看
- 当出现 ans > MAX_VALUE / 10 且 还有pop需要添加 时，则一定溢出
- 当出现 ans == MAX_VALUE / 10 且 pop > 7 时，则一定溢出，7是2^31 - 1的个位数

2. 从ans * 10 + pop < MIN_VALUE这个溢出条件来看
- 当出现 ans < MIN_VALUE / 10 且 还有pop需要添加 时，则一定溢出
- 当出现 ans == MIN_VALUE / 10 且 pop < -8 时，则一定溢出，8是-2^31的个位数

## 代码
```c++
class Solution {
public:
    int reverse(int x) {
        int max=2147483647;
        int min=-2147483648;
        int sum=0;
        int pop=0;
        while(x!=0){
            pop=x%10;
            x=x/10;
            //sum*10+pop>max => sum+pop/10>max/10
            //sum*10+pop<min => sum+pop/10<min/10
            /*if((sum==max/10 && pop<=max%10)||(sum==min/10 && pop>=min%10)){
                sum = sum*10 + pop;
            }else if(sum<max/10 && sum>min/10){
                sum = sum*10 + pop;
            }else{
                return 0;
            }*/
            
            //由于32位int型最大时首位只有1或2，可以省略尾数判断
            if(sum<=max/10 && sum>=min/10){
                sum = sum*10 + pop;
            }else{
                return 0;
            }
        }
        return sum;
    }
};
```
