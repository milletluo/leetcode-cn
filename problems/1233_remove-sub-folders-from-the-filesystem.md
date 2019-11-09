## [删除子文件夹(中等)](https://leetcode-cn.com/problems/remove-sub-folders-from-the-filesystem/)
<div class="notranslate"><p>你是一位系统管理员，手里有一份文件夹列表 <code>folder</code>，你的任务是要删除该列表中的所有 <strong>子文件夹</strong>，并以 <strong>任意顺序</strong> 返回剩下的文件夹。</p>

<p>我们这样定义「子文件夹」：</p>

<ul>
	<li>如果文件夹&nbsp;<code>folder[i]</code>&nbsp;位于另一个文件夹&nbsp;<code>folder[j]</code>&nbsp;下，那么&nbsp;<code>folder[i]</code>&nbsp;就是&nbsp;<code>folder[j]</code>&nbsp;的子文件夹。</li>
</ul>

<p>文件夹的「路径」是由一个或多个按以下格式串联形成的字符串：</p>

<ul>
	<li><code>/</code>&nbsp;后跟一个或者多个小写英文字母。</li>
</ul>

<p>例如，<code>/leetcode</code>&nbsp;和&nbsp;<code>/leetcode/problems</code>&nbsp;都是有效的路径，而空字符串和&nbsp;<code>/</code>&nbsp;不是。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>folder = ["/a","/a/b","/c/d","/c/d/e","/c/f"]
<strong>输出：</strong>["/a","/c/d","/c/f"]
<strong>解释：</strong>"/a/b/" 是 "/a" 的子文件夹，而 "/c/d/e" 是 "/c/d" 的子文件夹。
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>folder = ["/a","/a/b/c","/a/b/d"]
<strong>输出：</strong>["/a"]
<strong>解释：</strong>文件夹 "/a/b/c" 和 "/a/b/d/" 都会被删除，因为它们都是 "/a" 的子文件夹。
</pre>

<p><strong>示例 3：</strong></p>

<pre><strong>输入：</strong>folder = ["/a/b/c","/a/b/d","/a/b/ca"]
<strong>输出：</strong>["/a/b/c","/a/b/ca","/a/b/d"]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= folder.length&nbsp;&lt;= 4 * 10^4</code></li>
	<li><code>2 &lt;= folder[i].length &lt;= 100</code></li>
	<li><code>folder[i]</code>&nbsp;只包含小写字母和 <code>/</code></li>
	<li><code>folder[i]</code>&nbsp;总是以字符 <code>/</code>&nbsp;起始</li>
	<li>每个文件夹名都是唯一的</li>
</ul>
</div>

## 思路
1. 先排序，保证父文件夹在前面
2. 逐个遍历，如果一个文件夹后面的文件夹是该文件夹的子文件夹，置标志
3. 如果该文件夹已经被置标志了，跳过，否则超时
4. 将没有置标志的文件夹加入结果输出
   
## 代码
```c++
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
#define MIN(x, y) (((x) < (y)) ? (x) : (y))

// 假设a比b短，既判断b是否是a的子文件夹
bool isSubFolder(char* a, int lenA, char* b, int lenB)
{
    if((strncmp(a, b, lenA) == 0) && (b[lenA] == '/')){
        return true;
    }
    return false;
}

int cmp(const void *aa, const void *bb)
{
    char *a = *(char**)aa;
    char *b = *(char**)bb;
    return strcmp(a, b);
}
char ** removeSubfolders(char ** folder, int folderSize, int* returnSize){
    char **out = NULL;
    int count = 0;
    int flag[40000] = {0};
    
    qsort(folder, folderSize, sizeof(char*), cmp);
    
    for (int i = 0; i < folderSize; i++) {
        if (flag[i] == 1) {
            continue;
        }
        for (int j = i + 1; j < folderSize; j++) {
            if ((flag[i] == 0) && (flag[j] == 0) && 
                isSubFolder(folder[i], strlen(folder[i]), folder[j], strlen(folder[j]))) {
                flag[j] = 1;
            }
        }
    }
    for (int i = 0; i < folderSize; i++) {
        if (flag[i] == 0) {
            count++;
        }
    }
    // printf("%d\n",count);
    out = (char**)malloc(sizeof(char*) * count);
    for (int i = 0; i < count; i++) {
        out[i] = (char*)malloc(sizeof(char) * 100);
    }
    int idx = 0;
    for (int i = 0; i < folderSize && idx < count; i++) {
        // printf("fold = %s ==>",folder[i]);
        if (flag[i] == 0) {
            strcpy(out[idx], folder[i]);
            // printf("out = %s", out[idx]);
            idx++;
        }
    }
    *returnSize = count;
    return out;
}
```
