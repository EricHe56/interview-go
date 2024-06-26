# 冒泡排序

冒泡排序（Bubble Sort）也是一种简单直观的排序算法。它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端。

作为最简单的排序算法之一，冒泡排序给我的感觉就像 Abandon 在单词书里出现的感觉一样，每次都在第一页第一位，所以最熟悉。冒泡排序还有一种优化算法，就是立一个 flag，当在一趟序列遍历中元素没有发生交换，则证明该序列已经有序。但这种改进对于提升性能来说并没有什么太大作用。

## 1. 算法步骤

比较相邻的元素。如果第一个比第二个大，就交换他们两个。

对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。

针对所有的元素重复以上的步骤，除了最后一个。

持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

## 2. 动图演示

![](../../images/bubbleSort.b7d216a5.gif)

## 3. 最慢和最快

正序时最快，反序时最慢
## Golang实现

```go
func bubbleSort(arr []int) []int {
	if len(arr) == 0 {
		return arr
	}
	for i := 0; i < len(arr); i++ {
		for j := 0; j < len(arr); j++ {
			if arr[i] > arr[j] {
				arr[j], arr[i] = arr[i], arr[j]
			}
		}
	}
	return arr
}
```

上面原作者的实现不符合标准冒泡规则，下面bubbleSort1是我自己写的。他的那个函数会循环比较64次输出结果，我们只需要42次：
```golang
package main

import "fmt"

func bubbleSort(arr []int) []int {
	var t = 0
	if len(arr) == 0 {
		return arr
	}
	for i := 0; i < len(arr); i++ {
		for j := 0; j < len(arr); j++ {
			t++
			fmt.Println(t, "compare arr[i], arr[j]: ", i, j, arr[i], arr[j])
			if arr[i] > arr[j] {
				fmt.Println("arr[i] > arr[j] is True")
				arr[j], arr[i] = arr[i], arr[j]
			}
		}
	}
	return arr
}

func bubbleSort1(arr []int) []int {
	if len(arr) < 2 {
		return arr
	}
	var changed = true
	var t = 0
	for changed {
		changed = false
		for i := 0; i < len(arr)-1; i++ {
			t++
			fmt.Println(t, "compare arr[i], arr[i+1]: ", i, i+1, arr[i], arr[i+1])
			if arr[i] > arr[i+1] {
				arr[i], arr[i+1] = arr[i+1], arr[i]
				changed = true
			}
		}

	}
	return arr
}

func main() {
	var a = []int{1, 4, 6, 7, 8, 3, 2, 5}

	fmt.Println("Hello, 世界", bubbleSort1(a))
}

```



