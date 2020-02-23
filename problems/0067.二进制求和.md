## [二进制求和(简单)](https://leetcode-cn.com/problems/add-binary/)
<p>给定两个二进制字符串，返回他们的和（用二进制表示）。</p>

<p>输入为<strong>非空</strong>字符串且只包含数字&nbsp;<code>1</code>&nbsp;和&nbsp;<code>0</code>。</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入:</strong> a = "11", b = "1"
<strong>输出:</strong> "100"</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> a = "1010", b = "1011"
<strong>输出:</strong> "10101"</pre>

## 思路
取出两个字符串中较长的  
从后往前遍历，第一次遍历短的那一部分，有进位的处理进位  
第二次遍历长的字符串中余下的部分，如果最后有进位，在最前添1

## 代码
```c++
class Solution {
public:
    string addBinary(string a, string b) {
        int lenA=a.length();
        int lenB=b.length();
        if(lenB>lenA){
            swap(a,b);
            swap(lenA,lenB);
        }
        string out(a);//可以直接用a操作、返回
        int i,j;
        int c=0;
        for(i=lenA-1,j=lenB-1;j>=0;i--,j--){
            c=c+a[i]-'0'+b[j]-'0';
            out[i]=c%2+'0';
            c = c>=2 ? 1 : 0;
        }
        for(;i>=0;i--){
            c=c+a[i]-'0';
            out[i]=c%2+'0';
            c = c>=2 ? 1 : 0;
        }
        if(c==1){
            out.insert(0,1,'1');//out = '1' + out;
        }
        return out;
    }
};
```
## 其他思路
1. 首先让两个字符串等长，若不等长，在短的字符串前补零，否则之后的操作会超出索引。
2. 然后从后到前遍历所有的位数，同位相加，这里有一个点，用的是字符相加，利用 ASCII 码，字符在内部都用数字表示，我们不需要知道具体数值，但可知`‘0’-‘0’ = 0`，`‘0’+1=‘1’`，以此类推 。字符的加减，大小比较，实际上都是内部数字的加减，大小比较
3. 判断相加后的字符，若大于等于字符 `‘2’`，下一位需要进一
4. 第 0 位数的相加在这里是单独处理的，因为它可能涉及到字符的插入（即是否需要在最前面加一位数 ‘1’‘1’

## 代码
```c++
class Solution {
public:
    string addBinary(string a, string b) {
        int al = a.size();
        int bl = b.size();
        while(al < bl) //让两个字符串等长，若不等长，在短的字符串前补零，否则之后的操作会超出索引
        {
            a = '0' + a;
            ++ al;
        }
        while(al > bl)
        {
            b = '0' + b;
            ++ bl;
        }
        for(int j = a.size() - 1; j > 0; -- j) //从后到前遍历所有的位数，同位相加
        {
            a[j] = a[j] - '0' + b[j];
            if(a[j] >=  '2') //若大于等于字符‘2’，需要进一
            {
                a[j] = (a[j] - '0') % 2 + '0';
                a[j-1] = a[j-1] + 1;
            }
        }
        a[0] = a[0] - '0' + b[0]; //将ab的第0位相加
        if(a[0] >= '2') //若大于等于2，需要进一
        {
            a[0] = (a[0] - '0') % 2 + '0';
            a = '1' + a;
        }
        return a;
    }
};
```