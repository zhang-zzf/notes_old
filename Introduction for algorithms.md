##  TODO

1. 多路归并
2. s=x+y算法及s=x+y+z等

## 循环不变式

需证明一下3点

1. 初始化，循环的第一次迭代之前，它为真
2. 如果循环的某次迭代之前它为真，那么下次迭代之前它仍为真
3. 循环终止时，它为真

## 算法分析

预测算法需要的资源，通常是指时间度量，通过算法分析可以排除掉一些较差的实现。

## 算法设计

1. insertSort 属于增量排序
2. quickSort/mergeSort 属于分而治之排序

## Divide and Conquer

1. mergeSort 伪代码

   ```
   mergerSort(array, startIndex, endIndex) {
       if (startIndex < endIndex) {
           int mid = (startIndex + endIndex) / 2;
           mergeSort(array, startIndex, mid);
           mergeSort(array, mid + 1, endIndex)
           merge(array, startIndex, mid, endIndex);
       }
   }
   ```

2. mergeSort 最优和最坏的时间复杂度都是O(nlgn)

## 堆排序

#### 堆数据结构

A[1...n]

A.length 为数组长度

A.heap_size 为数组中堆大小

LEFT(i)：i的左孩子结点下标

RIGHT(i): i的右孩子结点下标

#### 维护堆

MAX_HEAPIFY 是用于维护最大堆的重要过程，它的输入为一个数组A和一个下标i，在调用MAX_HEAPIFY的时候，**我们假设根节点为LEFT(i)和RIGHT[i)的二叉树都是最大堆**。

**MAX_HEAPIFY 的时间复杂度为O(lgn)，也就是O(h)，h为堆的高度。**

##### MAX_HEAPIFY递归实现

```
MAX_HEAPIFY(A, i)
	l = LEFT(i)
	r = RIGHT(i)
	largest = i
	if existLeftChild
		if A[l] > A[largest]
			largest = l
		if existRightChild and A[r] > A[largest]
			largest = r
	if largest not equal i
		swap A[i] with A[largest]
		MAX_HEAPIFY(A, largest)
```

#####  MAX_HEAPIFY循环实现

```
MAX_HEAPIFY(A, i)
	while hasLeftChild(i)
		l = LEFT(i)
		r = RIGHT(i)
		largest = i
		if A[l] > A[largest]
			largest = l
		if hasRightChild(i) and A[r] > A[largest]
			largest = r
		if largest == i
			break
		else
			swap A[i] with A[largest]
			i = largest
```

#### 建堆

我们可以利用自底向上的方法利用过程MAX_HEAPIFY把一个大小为n=A.length的数组A[1...n]转换为最大堆。由于n/2之后的元素都是叶子，只需对**n/2和之前**的元素调用MAX_HEAPIFY即可建立大堆。

**时间复杂度为O(nlgn)，更紧确的界是O(n)。**因此我们可以认为是在**线性时间内把无序数组构建成最大堆。**

##### BUILD_MAX_HEAP

```
BUILD_MAX_HEAP(A)
 for i=⌊n/2⌋ downto 1
 	MAX_HEAPIFY(A, i)
```

#### 插入法建堆

每次插入之前是一个大堆，MAX_HEAP_INSERT之后依然是一个大堆。

**循环不变式 A[1, i-1]是大堆，插入i元素到A中，A[1,i]是大堆。**

##### MAX_HEAP_INSERT

```
MAX_HEAP_INSERT(A, x)
	A[++heap_size]=x
	for i=heap_size; i>1 and A[PARENT(i)]<x; i=PARENT(i) // 向上调整堆
		A[i]=A[PARENT(i)]
	A[i]=x
```

##### BUILD_MAX_HEAP_USE_INSERT

```
BUILD_MAX_HEAP_USE_INSERT(A)
	A.heap_size=0
	for x in A
		MAX_HEAP_INSERT(A,x)
```

#### 堆排序算法

调用BUILD_MAX_HEAP先把无序数组建立成大堆，A[1]便是数组中最大的元素。

i从n递减到1，每次交换A[1]和A[i]，把A.heap_size -=1然后MAX_HEAPIFY(A, 1)。

循环不变式：A[1...heap_size]依然是大堆（A[1] 依旧是A[1,heap_size]中的最大元素），A[i...n]是有序（A[i] ≤ A[i+1] ≤ ... ≤ A[n]）且A[i...n]为最终有序（A[n]为A[1...n]的最大值）

**时间复杂度为O(nlgn)**

##### HEAP_SORT

```
HEAP_SORT(A)
  BUILD_MAX_HEAP(A)
  for i=n downto 1
  	swap A[i] with A[1]
  	A.heap_size -= 1
  	MAX_HEAPIFY(A, 1)
```

## 优先队列（Priority Queue）

优先队列是一种维护由一组数据元素构成的集合S的数据结构，每个元素有一个权值，抽象数据结构如下

INSERT(S, x)：把x元素（k为其权值）插入到S中

MAXIMUM(S)：返回S集合中具有最大权值的元素

EXTRACT_MAX(S)：取出S集合中的最大权值的元素

MODIFY_KEY(S, x, k2)：增大或较小x元素的k值

### 链式存储结构

> ?1：lastInsert无法移动到右边的相邻节点

```
Node {
  Node parent
  X x
  Node leftChild
  Node rightChild
}
```

```
PriorityQueue {
  Node header
  Node lastInsert
  int size
}
```

#### INSERT(S,x)

```
INSERT(S,x)
	Node nodex = Node(lastInsert, x, null, null)
	if lastIndex.leftChild == null
		lastIndex.leftChild = nodex
	else if lastIndex.rightChild == null
		lastIndex.rightChild = nodex
	else
```

### 顺序存储结构

 ```
PriorityQueue {
  int length
  int heap_size
  X[] array
}
 ```

#### INSERT(S,x)

```
INSERT(S, x)
	ensureCapacity()
	S[++heap_size] = x
	for (i = heap_size; i>=1 and S[i] > S[PARENT(i)]; i = PARENT(i))
		MAX_HEAPIFY(S, PARENT(i))
```

#### MAXIMUM(S)

```
MAXIMUM(S)
	return S[1]
```

#### EXTRACT_MAX(S)

```
EXTRACT_MAX(S)
	X ret = S[1]
	S[1] = S[heap_size]
	heap_size -= 1
	MAX_HEAPIFY(S, 0)
	return ret
```

#### MODIFY_KEY(S, x, k2)

```
MODIFY_KEY(S, x, k2)
	i = findXIndex(S, x)
	if (S[i].k > k2) // k值变小
		S[i].k = k2
		MAX_HEAPIFY(S, i) // 向下调整堆
	else if (S[i].k < k2) // k值变大
		S[i].k = k2
		for (j=i;j>=1 and S[j] > S[PARENT[j]];j=PARENT(j)) // 向上调整堆
			MAX_HEAPIFY(S, PARENT(j))
```

#### HEAP_DELETE

```
算法是错误的，不满足完全二叉树
HEAP_DELETE(S, i)
	l = LEFT(i)
	r = RIGHT(i)
	largest = i
	if l ≤ S.heap_size
		largest = l
		if r ≤ S.heap_size and S[r] > S[l]
			largest = r
	if laregest != i
		S[i] = S[largest]
		HEAP_DELETE(S, largest)
	else
		S.heap_size -= 1		
```

```
HEAP_DELETE(S, i)
	if (S[i] > S[heap_size]) // 向下调整堆
		S[i] = S[heap_size]
		MAX_HEAPIFY(S, i)	// lgn
	else if (S[i] < S[heap_size]) // 向上调整堆
		S[i] = S[heap_size]
		pivot = S[i]
		for (j=i; j>1 and S[PARENT(j)]<pivot; j=PARENT(j))
			S[j] = S[PARENT(j)]
		S[PARENT(j)] = pivot // very import
	S.heap_size -= 1
```

## d-ary heap

A **_$d$-ary heap_** is like a binary heap, but (with one possible exception) non-leaf nodes have $d$ children instead of $2$ children.

We can represent a $d$-ary heap in a $1$-dimensional array as follows. The root resides in $A[1]$, its $d$ children reside in order in $A[2]$ through $A[d + 1]$, their children reside in order in $A[d + 2]$ through $A[d^2 + d + 1]$, and so on. The following two procedures map a node with index $i$ to its parent and to its $j$ th child (for $1 \le j \le d$), respectively.

```cpp
d-ARY-PARENT(i)
    return floor((i - 2) / d + 1)
```

```cpp
d-ARY-CHILD(i, j)
    return d(i - 1) + j + 1
```

## 快速排序-quick_sort

快速排序采用分治法（DIVIDE AND CONQUER)。平均O(nlgn)，最坏O(n²)

**分解：**A[p..r]被划分为2个子数组A[p..q-1]和A[q+1..r]（子数组有可能为空）使得A[p..q-1]中的每个元素都≤A[q]，并且A[q]≤A[q+1..r]中的每个元素。其中计算下标q也是划分过程的一部分。

**解决：**通过递归调用快速排序，对子数组A[p..q-1]和A[q+1..r]进行排序。

**合并：**子数组是原址排序，不需要合并操作，A[p..r]已经有序。

### 分区-PARTION

取pivot，小的放pivot左边，大的放pivot右边，俗称分区过程。递归排序左边子序列和右边子序列。

#### 循环不变式：A[pivot_index...right] ≥A[right]

**此不变式是错误的，初始化时不能满足。但下面的算法是正确的**

```cpp
PARTITION(A, left, right) pivot_index
	pivot_index=left
	for i=left upto right-1
		if A[i]<A[right]
			swap(A, pivot_index, i)
			pivot_index+=1
	swap(A, pivot_index, right)
```

#### 循环不变式：A[left..pivot_index]<A[right]

```
PARTITION(A, left, right) return pivot_index
	pivot_index=left-1
	for i=left upto right-1
		if A[i]<A[right]
			swap(A, pivot_index++, i)
	swap(A, pivot_index++, right)
```

### QUICK_SORT

```go
QUICK_SORT(A, left, right)
	if (left<right)
    pivot_index=PARTITION(A, left, right)  	// divide
    QUICK_SORT(A, left, pivot_index-1)		// conquer left
    QUICK_SORT(A, left, pivot_index+1)		// conquer right
```

### 快速排序的随机化版本

```
RANDOMIZED_PARTITION(A, p, r)
	i=RANDOM(p, r)
	exchange A[r] with A[i]
	return PARTITION(A, p, r)

QUICK_SORT(A, left, right)
	if (left<right)
		q=RANDOMIZED_PARTITION(A, left, right)
		QUICK_SORT(A, left, q-1)
		QUICK_SORT(A, q+1, right)
```

### 快速排序数组存在相同元素的优化版本

Invariant: A[p..q]<A[r], A[q+1..t]=A[r], A[t+1..i]>A[r], A[i+1..r-1] unknown

```
PARTITION'(A, p, r)
	t=q=p-1
	for i=q upto r-1
		if A[i]≤A[r]
			t+=1
			exchange A[t] with A[i]
			if A[t]<A[r]
				q+=1
				exchange A[q] with A[t]
	t+=1
	exchange A[t] with A[r]
	return (q+1, t)

QUICK_SORT'(A, p, r)
	if p<r
    equal_1, equal_2=PARTITION'(A, p, r)
    QUICK_SORT'(A, p, equal_1-1)
    QUICK_SORT'(A, equal_2+1, r)
```

### 快速排序 尾递归实现

最坏栈深度为n

```
TAIL_RECURSIVE_QUICK_SORT(A, p, r)
	while p<r
		// partition and sort left subarray
		q=PARTITION(A, p, r)
		TAIL_RECURSIVe_QUICK_SORT(A, p, q-1)
		p=q+1
```

### 快速排序 尾递归实现优化版本

最坏栈深度为lgn

```
TAIL_RECURSIVE_QUICK_SORT'(A, p, r)
	while p<r
		// partition and sort the small  
    q=PARTITION(A, p, r)
    if q-p<r-q
      TAIL_RECURSIVE_QUICK_SORT'(A, p, q-1)
      p=q+1
    else
      TAIL_RECURSIVE_QUICK_SORT'(A, q+1, r)
      r=q-1
```

### 计数排序 Counting-sort

假设n个输入元素中的每一个元素都是[0,k]区间的一个整数，k为一个整数，当**k=O(n**)时，排序的**运行时间为O(n)**

计数排序的思想：通过中间记录直接找到元素的位置

```
COUNTINT_SORT(A, k)
	init Array C with length of k
	for i=1 to A.length
		C[A[i]]+=1
	for i=2 to C.length
		C[i]+=C[i-1]
	// 必须倒序，稳定排序
	for i=A.length to 1		
  	B[C[A[i]]]=A[i]
  for i=1 to A.length
  	A[i]=B[i]
```

**稳定排序/非原址排序/时间复杂度为O(n)但是常量因子大（4）**



### 基数排序 Radix-sort

```c++
RADIX_SORT(A, d):
	for i=1 to d
		use a stable sort to sort array A on digit i
```


## 数据结构

### 基本数据结构

#### 栈 stack

栈的数组实现S[1..n]，S.top指向栈顶元素，S.top=0时表示空栈，S.top=n时表示满栈。

##### STACK_EMPTY

```c++
STACK_EMPTY(S)
	if S.top=0
		return true
	return false
```

##### STACK_FULL

```c++
STACK_FULL(S)
	if S.top=n
		return true
	return false
```

##### PUSH

```c++
PUSH(S, x)
	if STACK_FULL(S)
		error "stack is full"
	S[++S.top]=x		
```

##### POP

```c++
POP(S)
	if STACK_EMPTY(S)
		error "stack is empty"
	return S[S.top--]
```

#### 队列 queue

循环队列的数组实现Q[1..n]，Q.size表示队列的大小（Q.size<=n），Q.head表示队列的头，Q.tail表示队列的尾

##### QUEUE_INIT

```
QUEUE_INIT(Q)
  Q.size=0
  Q.head=1
  Q.tail=1
```

##### EMPTY/FULL

```
QUEUE_EMPTY(Q)
	return Q.size==0

QUEUE_FULL(Q)
	return Q.size==n
```

##### ENQUEUE

```c++
ENQUEUE(Q, x)
	if QUEUE_FULL(Q)
		error "queue is full"
	Q[Q.tail]=x
	Q.size+=1
	Q.tail=(Q.tail+1)%n
```

##### DEQUEUE

```c++
DEQUEUE(Q)
  if QUEUE_EMPTY(S)
    error "queue is empty"
	x=Q[Q.head]
	Q.size-=1
	Q.head=(Q.head+1)%n
	return x
```

Q[1..n]容纳n-1个元素时，只需要Q.head表示队列的头，Q.tail表示队列的尾

##### QUEUE_INIT

```
QUEUE_INIT(Q)
  Q.head=1
  Q.tail=1
```

##### EMPTY/FULL

```
QUEUE_EMPTY(Q)
	return Q.tail==Q.head

QUEUE_FULL(Q)
	return Q.tail+1==Q.head
```

##### ENQUEUE

```c++
ENQUEUE(Q, x)
	if QUEUE_FULL(Q)
		error "queue is full"
	Q[Q.tail]=x
	Q.tail=(Q.tail+1)%n
```

##### DEQUEUE

```c++
DEQUEUE(Q)
  if QUEUE_EMPTY(S)
    error "queue is empty"
	x=Q[Q.head]
	Q.head=(Q.head+1)%n
	return x
```

#### 双端队列 deque

数组实现：DQ[1..n]，DQ.header表示队头，DQ.tailer表示队尾。

DQ.header==DQ.tailer 空队列；(DQ.tailer+1)%n==DQ.header 满队列。

##### DEQUE_INIT

```
DEQUE_INIT(DQ)
	DQ.header=1
	DQ.tailer=1
```

##### DEQUE_FULL / DEQUE_EMPTY

```c++
DEQUE_FULL(DQ)
 return (DQ.tailer+1)%n==DQ.header

DEQUE_EMPTY(DQ)
	return DQ.tailer==DQ.header
```

##### ENDEQUE_TAILER

```c++
ENDEQUE_TAILER(DQ, x)
	if DEQUE_FULL(DQ)
		error "full"
	DQ[DQ.tailer]=x
	DQ.tailer=(DQ.tailer+1)%n
```

##### ENDEQUE_HEADER

```c++
ENDQUUE_HEADER(DQ, x)
	if DEQUE_FULL(DQ)
		error "full"
	//DQ[DQ.header]=x   // error, header should always point to the first element.
	DQ.header-=1
	if DQ.header==0
		DQ.header=n
	DQ[DQ.header]=x
```

##### DEDEQUE_HEADER

```c++
DEDEQUE_HEADER(DQ)
	if DEQUE_EMPTY(DQ)
		error "empty"
	x=DQ[DQ.header]
	DQ.header=(DQ.header+1)%n
	return x
```

##### DEDEQUE_TAILER

```c++
DEDEQUE_TAILER(DQ)
	if DEQUE_EMPTY(DQ)
		error "empty"
	x=DQ[DQ.tailer-1]
	DQ.tailer-=1
	if DQ.tailer==0
		DQ.tailer=n
	return x
```

#### 有根树

#####  2叉树O(n) 遍历

```c++
TRAVEL_TREE(node)
	if node!=NIL
		print node.key
		TRAVEL_TREE(node.left)
		TRAVEL_TREE(node.right)
		
TRAVEL_TREE(node)
	if node==NIL
		return
	PUSH(S, node)
	while !STACK_EMPTY(S)
		n=POP(S)
		print n.key
		if n.right!=NIL
			PUSH(S, n.right)
		if n.left!=NIL
			PUSH(S, n.left)
```

##### 分支无限制的有根树 O(n)遍历

左孩子，右兄弟表示法。node.parent指向父节点，node.left_child指向node的最左边的孩子节点，node.right_child指向node右侧相邻的兄弟节点。

```c++
TRAVEL_TREE(node)
	if node!=NIL
		print node.key
		TRAVEL_TREE(node.right_child)
		TRAVEL_TREE(node.left_child)
```



