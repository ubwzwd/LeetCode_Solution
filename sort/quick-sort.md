# Quick Sort

### 快速排序基本思路

#### 核心思想：分治（Divide and Conquer）

1. 选择枢轴（Pivot/Seed）：从数组中选一个元素作为基准
2. 分区（Partition）：把数组分成两部分

* 左边：所有 ≤ pivot 的元素
* 右边：所有 > pivot 的元素

1. 递归排序：对左右两部分分别递归执行快速排序



overall process looks like this:

\[left, i)                                          \[i,   j)                                 \[j , right)                   right

elements <= pivot                     elements > pivot               not visited yet         pivot

```
// sudo code
init i = left, j = left
every time check element j
if element j <= pivot:
  swap i and j
  i++, j++
if element j > pivot:
  j++ 
```

