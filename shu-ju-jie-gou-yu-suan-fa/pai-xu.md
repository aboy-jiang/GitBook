---
description: 轻松理解简单排序
---

# 排序

## 定义

将`value`插入`a[i]`、`a[i+1]`之间，使得`a[i] < value < a[i+1]`

## 插入排序

#### 思路：

1. 将待排序数组分为`[0, 1)`和`[1, n)`两组，即为A和B
2. 遍历B组，每次取其第1个元素，插入到A组（结果：`A组元素数+1`，`B组元素数-1`）
3. 直到A组为`[0, n)`B组为`空`排序完成

#### 插入方法：

* **直接插入**：先移动，再插入
  * 遍历 `j从 A组最后一个位置 --> 0`若`j >= 0 && value < a[j]`移动`a[j+1]=a[j]` 遍历结束后`j`指向待插入位置`前一个`位置
  * 插入`a[j+1] = value`
* **折半插入**：先折半查找，再移动，最后再插入
  * 在A组中用折半查找，找到插入位置`low`
  * 遍历 `j从 A组最后一个位置 --> low`若`j >= low`移动`a[j+1]=a[j]`遍历结束后`j`指向待插入位置`前一个`位置
  * 插入`a[j+1] = value`

#### 代码实现：

```c
#include <stdio.h>

void insert_sort(int a[], int n);
void binary_insert_sort(int a[], int n);

int main(int argc, char *argv[]) 
{
	int a[] = {1, 21, 4, 3};
	int n = 4, i;
	// insert_sort(a, n);
	binary_insert_sort(a, n);
	for (i = 0; i < n; i++) {
		printf("%d ", a[i]);
	}
	return 0;
}

void insert_sort(int a[], int n) 
{
	int i, j, value;
	for (i = 1; i < n; i++) { // A:[0,i-1] B:[i,n-1]，遍历B组
		value = a[i]; // 取B组第一个元素为待插入元素

		// 先移动、在插入
		j = i - 1; // j从（B组第一个元素前一个位置） A组最后一个位置 --> 0
		while (j >= 0 && a[j] > value) { // 凡是大于value（B组第一个元素）的元素
			a[j+1] = a[j]; // 全部向后移动一个位置
			j--;
		}
		a[j+1] = value;
	}
}

void binary_insert_sort(int a[], int n) 
{
	int i, j, value, low, high, mid;

	for (i = 1; i < n; i++) { // A:[0,i-1] B:[i,n-1]，遍历B组
		value = a[i]; // 取B组第一个元素为待插入元素

		// 先折半查找，查找到待插入位置
		low = 0, high = i - 1;
		while (low <= high) {
			mid = (low + high) / 2;
			if (value < a[mid])
				high = mid - 1;
			else
				low = mid + 1;
		}

		// 再移动，最后再插入
		j = i - 1; // j从（B组第一个元素前一个位置） A组最后一个位置 --> 0
		while (j >= low) { // 待插入位置low后面的元素
			a[j+1] = a[j]; // 全部向后移动一个位置
			j--;
		}
		a[j+1] = value; // 注：这里low == j+1，因此用a[low] = value 也是可以的
	}
}
```

>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x5206;&#x6790;&#xFF1A;</b>
      </th>
      <th style="text-align:left">&#x76F4;&#x63A5;&#x63D2;&#x5165;</th>
      <th style="text-align:left">&#x6298;&#x534A;&#x63D2;&#x5165;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x7A33;&#x5B9A;&#x6027;</td>
      <td style="text-align:left">&#x7A33;&#x5B9A;</td>
      <td style="text-align:left">&#x7A33;&#x5B9A;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6392;&#x5E8F;&#x603B;&#x8D9F;&#x6570;</td>
      <td style="text-align:left"><code>i</code>&#x4ECE;<code>1</code>&#x5230;<code>n-1</code>&#xFF0C;&#x5171;<code>n-1</code>&#x8D9F;</td>
      <td
      style="text-align:left"><code>i</code>&#x4ECE;<code>1</code>&#x5230;<code>n-1</code>&#xFF0C;&#x5171;<code>n-1</code>&#x8D9F;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6BD4;&#x8F83;&#x6B21;&#x6570;</td>
      <td style="text-align:left">
        <p>&#x5347;&#x5E8F;&#xFF1A;&#x7B2C;<code>i</code>&#x8D9F;&#x4EC5;&#x6BD4;&#x8F83;<code>1</code>&#x6B21;&#xFF0C;&#x603B;&#x6B21;&#x6570;
          =<code>n-1</code>
        </p>
        <p>&#x964D;&#x5E8F;&#xFF1A;&#x7B2C;<code>i</code>&#x8D9F;&#x9700;&#x6BD4;&#x8F83;<code>i</code>&#x6B21;&#xFF0C;&#x603B;&#x6B21;&#x6570;
          =</p>
      </td>
      <td style="text-align:left">&#x7B2C;<code>i</code>&#x8D9F;&#x9700;&#x6BD4;&#x8F83;&#x6B21;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x65F6;&#x95F4;&#x590D;&#x6742;&#x5EA6;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7A7A;&#x95F4;&#x590D;&#x6742;&#x5EA6;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

## 选择排序

**思路：**

1. 将待排序数组分为`空`和`[0, n)`两组，记为A和B
2. 遍历B组，找到最小元素位置`min`，**交换**B组`0`和`min`两个位置的元素（结果：`A组元素数+1`，`B组元素数-1`）
3. 直到A组为`[0, n-1)`B组只剩`n`这一个元素，排序完成

#### 代码实现：

```c
#include <stdio.h>

void select_sort(int a[], int n);
void swap(int *a, int *b);

int main(int argc, char *argv[]) 
{
	int a[] = {1, 21, 4, 3};
	int n = 4, i;
	select_sort(a, n);
	for (i = 0; i < n; i++) {
		printf("%d ", a[i]);
	}
	return 0;
}

void select_sort(int a[], int n) {
	int i, j, min;

	for (i = 0; i < n - 1; i++) {
		min = i;
		for (j = i + 1; j < n; j++) {
			if (a[j] < a[min]) // 发现比a[min]小的元素 
				min = j;
		}
		if (min != i) {
			swap(a + min, a + i);
		}
	}
}

void swap(int *a, int *b) 
{
	int t = *a;
	*a = *b;
	*b = t;
}
```

| 分析： | 选择排序 |
| :--- | :--- |
| 稳定性 | 不稳定（交换在不相邻元素间进行） |
| 排序总趟数 | `i`从`0`到`n-2`，共`n-1`趟 |
| 比较次数 | 第`i`趟需比较`n-1-i`次，总次数 = $$\frac{n(n-1)}{2}$$ |
| 时间复杂度 | $$O(n^2)$$ |
| 空间复杂度 | $$O(1)$$ |

## 冒泡排序

**思路：**

1. 将待排序数组分为`[0, n)`和`空`两组，即为A和B
2. 遍历A组，依次两两比较，若`a[i] > a[i+1]`**交换**两者位置，全部比较完之后，A组中最大者将移动到最后（结果：`A组元素数-1`，`B组元素数+1`）
3. 直到A组只剩`0`B组为`[1, n)`排序完成
4. \[注\]：若在某一次遍历A组中，只有比较没有交换，则说明A组中各元素已排好序（升序），用一个flag标示是否发生交换，来决定是否终止后续比较。

```c
#include <stdio.h>

void bubble_sort(int a[], int n);
void swap(int *a, int *b);

int main(int argc, char *argv[]) 
{
	int a[] = {1, 21, 4, 3};
	int n = 4, i;
	bubble_sort(a, n);
	for (i = 0; i < n; i++) {
		printf("%d ", a[i]);
	}
	return 0;
}

void bubble_sort(int a[], int n) 
{
	int i, j, flag = 1;

	j = n - 1;
	while (j > 0 && flag) {
		flag = 0;
		for (i = 0; i < j; i++) {
			if (a[i] > a[i+1]) {
				swap(a + i, a + i + 1);
				flag = 1;
			}
		}
		j--;
	}
}

void swap(int *a, int *b) 
{
	int t = *a;
	*a = *b;
	*b = t;
}
```

| 分析： | 选择排序 |
| :--- | :--- |
| 稳定性 | 稳定（交换在相邻元素间进行） |
| 排序总趟数 | 【最坏】倒序：`j`从`n-1`到`1`，共`n-1`趟 |
|  | 【最好】已排好序：1趟 |
| 比较次数 | 【最坏】第`i`趟需比较`n-i`次，总次数 = $$\frac{n(n-1)}{2}$$ |
|  | 【最好】n-1次 |
| 时间复杂度 | $$O(n^2)$$ |
| 空间复杂度 | $$O(1)$$ |

## 希尔排序

**思路：**

1. 依次将待排序数组按照间隔 `gap`\($$\frac{n}{2}$$, $$\frac{n}{4 }$$, $$\frac{n}{8}$$, ..., 1\)，分成`n-gap`个子组，每次都对各个子组进行排序。
2. 当完成最后一次`gap=1`时的排序后，排序完成。

注：`gap`分组方式不同，算法性能也有所不同。对子组进行排序，可选插入排序、冒泡排序、选择排序等，下面算法选取冒泡排序实现。

#### 代码实现：

```c
#include <stdio.h>

void shell_sort(int a[], int n);
void swap(int *a, int *b);

int main(int argc, char *argv[]) 
{
	int a[] = {11, 21, 4, 3};
	int n = 4, i;
	shell_sort(a, n);
	for (i = 0; i < n; i++) {
		printf("%d ", a[i]);
	}
	return 0;
}

void shell_sort(int a[], int n) 
{
	int i, flag;
	int gap = n;
	while (gap > 1) {
		gap /= 2;
		flag = 1;
		while (flag) { // 这里不同上面的冒泡排序，没有j>0的条件判断
			flag = 0;
			for (i = 0; i < n - gap; i++) { // 是因为这里同时对多个分组混合进行冒泡排序
				if (a[i] > a[i + gap]) {
					swap(a + i, a + i + gap);
					flag = 1;
				}
			}	
		}
	}
}

void swap(int *a, int *b) 
{
	int t = *a;
	*a = *b;
	*b = t;
}
```

| 分析： | 选择排序 |
| :--- | :--- |
| 稳定性 | 不稳定（交换在不相邻元素间进行） |
| 排序总趟数 | `i`从$$\frac{n}{2}$$到`1`，共$$\lfloor\log_2{n}\rfloor$$趟 |
| 比较次数 | 不讨论 |
| 时间复杂度 | $$O(n\log_2{n})$$与$$O(n^2)$$之间，约为$$O(n^{1.23})$$ |
| 空间复杂度 | $$O(1)$$ |

## 快速排序

**思路：**

1. 选取数组`最后1个`元素作为中心点`pivot`，将数组中比`pivot`小的元素都移动到`pivot`左侧，比`pivot`大的元素都移动到右侧。
2. 移动完成之后，`pivot`将整个数组分为左右两个数组A、B，分别对A、B进行步骤1操作（递归）。
3. 直到A、B中`元素个数 <= 1`排序完成

**代码实现：**

```c
#include <stdio.h>

void quick_sort(int a[], int n);
void quick_sort_t(int a[], int low, int high);
void swap(int *a, int *b);

int main(int argc, char *argv[]) 
{
	int a[] = {1, 2, 4, 3};
	int n = 4, i;
	quick_sort(a, n);
	for (i = 0; i < n; i++) {
		printf("%d ", a[i]);
	}
	return 0;
}

void quick_sort(int a[], int n) {
	quick_sort_t(a, 0, n - 1);
}

void quick_sort_t(int a[], int low, int high) {
	if (low >= high) return;

	int pivot = high, i = low, j = high - 1, t;
	while (1) {
		while (i < high && a[i] <= a[pivot]) i++;
		while (j > low && a[j] > a[pivot]) j--;
		if (i < j) {
			swap(a + i, a + j);
		} else {
			break;
		}
	}
	swap(a + i, a + pivot);

	quick_sort_t(a, low, i - 1);
	quick_sort_t(a, i + 1, high);
}

void swap(int *a, int *b) {
	int t = *a;
	*a = *b;
	*b = t;
}
```

>

| 分析： | 选择排序 |
| :--- | :--- |
| 稳定性 | 不稳定（交换在不相邻元素间进行） |
| 排序总趟数 | 【最大】原数组有序：n趟（最大递归深度） |
|  | 【最小】每趟排序选取的pivot正好将数组左右平分：$$log_2n$$趟（最小递归深度） |
| 比较次数 | 【最大】第`i`趟需比较`n-i`次，总次数 = $$\frac{n(n-1)}{2}$$ |
|  | 【最小】不讨论 |
| 时间复杂度 | 【最大】：$$O(n^2)$$  |
|  | 【最小】$$O(n\log_2{n})$$ |
| 空间复杂度 | $$O(1)$$ |

## 堆排序

**思路：**

1. [推荐视频](https://www.youtube.com/watch?v=j-DqQcNPGbE)：[https://www.youtube.com/watch?v=j-DqQcNPGbE](https://www.youtube.com/watch?v=j-DqQcNPGbE)

**代码实现：**

```c
void swap(int tree[], int i, int j) {
    int temp = tree[i];
    tree[i] = tree[j];
    tree[j] = temp;
}

/*
 * 使一颗完全二叉树的第i个结点为根节点的子树变成一颗稳定的堆树
 * 第i个结点
 * c1 = 2 * i + 1;
 * c2 = 2 * i + 2;
 * */
void heapify(int tree[], int n, int i) {
    if (i >= n) return;
    int c1 = 2 * i + 1;
    int c2 = 2 * i + 2;
    int max = i;
    if (c1 < n && tree[c1] > tree[max])
        max = c1;
    if (c2 < n && tree[c2] > tree[max])
        max = c2;
    if (max != i) { 
        swap(tree, max, i);
        heapify(tree, n, max);
    } 
}

/*
 * 构建堆
 * 从最后一个结点的parent结点开始直到根结点，分别对其做heapify操作
 * last_node = n - 1;
 * parent = (last_node - 1) / 2;
 * */
void build_heap(int tree[], int n) {
    int last_node = n - 1;
    int parent = (last_node - 1) / 2;
    
    for(int i = parent; i >= 0; i--) {
        heapify(tree, n, i);
    }
}

void heap_sort(int tree[], int n) {
    build_heap(tree, n);
    for (int i = n - 1; i >= 0; i--) {
        swap(tree, i, 0);
        heapify(tree, i, 0);    
    }
}
```



| 分析： | 选择排序 |
| :--- | :--- |
| 稳定性 | 不稳定（交换在不相邻元素间进行） |
| 排序总趟数 | `i`从`n-1`到`1`，共`n-1`趟 |
| 比较次数 | 不讨论 |
| 时间复杂度 | $$O(n\log_2{n})$$ |
| 空间复杂度 | $$O(1)$$ |

