# 常用C++ STL算法
`#include <algorithm>`

swap:交换存储在两个对象中的值。

max:返回两个元素中较大一个。

min:返回两个元素中较小一个。

sort:以升序重新排列指定范围内的元素。

默认升序排序，但可以使用重载版本改变规则：

如：
```
bool cmp(int a,int b){

     return a>b;//改变规则为降序

}

sort（array,array+n,cmp）;
```
 

对于非基础数据结构，以结构体为例，重载sort函数
```
struct node{
     int c;
}

bool cmp(node a,node b){
       return a.c>b.c;
}

sort(array,array+n,cmp);
```
# 常用C++ STL容器
## vector
`#include <vector>`
1. push_back(x) 在数组的最后添加元素x
2. pop_back() 删除最后一个元素，无返回值
3. at(i) 返回位置i的元素
4. begin() 返回一个迭代器，指向第一个元素
5. end() 返回一个迭代器，指向最后一个元素的下一个位置
6. front() 返回数组头的引用
7. capacity(x) 为vector分配空间 
8. size() 返回数组大小 
9. resize(x) 改变数组大小，如果x比之前分配的空间大，则自动填充默认值
10. insert 插入元素 
- a.insert(a.begin(),10); 将10插入到a的起始位置前
- a.insert(a.begin(),3,10) 将10插入到数组位置的0-2处
11. erase 删除元素 
- a.erase(a.begin()); 将起始位置的元素删除
- a.erase(a.begin(),begin()+2); 将0~2之间的元素删除
12. rbegin() 返回一个逆序迭代器，它指向最后一个元素
13. rend() 返回一个逆序迭代器，它指向的第一个元素前面的位置
14. clear()清空所有元素
15. 二维数组初始化
```
vector<vector<int>> matrix(row);
for(int i=0;i<row;i++) {
    matrix[i].resize(col);
}
```

## set
`#include <set>`
1. begin() 返回一个迭代器，指向第一个元素。 
2. end() 返回一个迭代器，指向最后一个元素的下一个位置。 
3. clear()清空set的所有元素。 
4. empty() 判断是否为空。 
5. size() 返回当前元素个数 
6. erase(it) 删除迭代器指针it指向的元素。 
7. insert(a) 插入元素a 
8. count() 查找某个元素出现的次数，只有可能为0或1。 
9. find() 查找某个元素出现的位置，如果找到则返回这个元素的迭代器，如果不存在，则返回s.end()

## queue
`#include <queue>`
1. q.push(x) 将元素x置于队列的末端 
2. q.pop() 同样不会返回弹出元素的值 
3. q.front() 返回队首元素 
4. q.back() 返回队尾元素
5. q.empty() 判断是否为空 
6. q.size() 返回队列元素个数

## stack
`#include <stack>`
1. s.pop() 出栈，注意并不返回出栈的元素 
2. s.push(x) 进栈
3. s.top() 访问栈顶元素
4. s.empty() 判断栈空，栈为空时返回true 
5. s.size() 返回栈中元素个数