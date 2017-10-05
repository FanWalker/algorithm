# 堆排序

工作原理：把最大堆堆顶的最大数取出，将剩余的堆继续调整为最大堆，再次将堆顶的最大数取出，这个过程持续到剩余数只有一个时结束。



## 堆排序算法流程

在堆的数据结构中，堆中的最大值总是位于根节点(在优先队列中使用堆的话堆中的最小值位于根节点)。堆中定义以下几种操作：

1、最大堆调整（Max_Heapify）：将堆的末端子节点作调整，使得子节点永远小于父节点

2、创建最大堆（Build_Max_Heap）：将堆所有数据重新排序

3、堆排序（HeapSort）：移除位在第一个数据的根节点，并做最大堆调整的递归运算



## JavaScript语言实现

	Array.prototype.heap_sort = function() {
		var arr = this.slice(0);
		function swap(i, j) {
			var tmp = arr[i];
			arr[i] = arr[j];
			arr[j] = tmp;
		}
	
		function max_heapify(start, end) {
			//建立父節點指標和子節點指標
			var dad = start;
			var son = dad * 2 + 1;
			if (son >= end)//若子節點指標超過範圍直接跳出函數
				return;
			if (son + 1 < end && arr[son] < arr[son + 1])//先比較兩個子節點大小，選擇最大的
				son++;
			if (arr[dad] <= arr[son]) {//如果父節點小於子節點時，交換父子內容再繼續子節點和孫節點比較
				swap(dad, son);
				max_heapify(son, end);
			}
		}
	
		var len = arr.length;
		//初始化，i從最後一個父節點開始調整
		for (var i = Math.floor(len / 2) - 1; i >= 0; i--)
			max_heapify(i, len);
		//先將第一個元素和已排好元素前一位做交換，再從新調整，直到排序完畢
		for (var i = len - 1; i > 0; i--) {
			swap(0, i);
			max_heapify(0, i);
		}
	
		return arr;
	};
	var array = [80, 93, 60, 12, 42, 30, 68, 85, 10];
	console.log(array.heap_sort());
	
	//[ 10, 12, 30, 42, 60, 68, 80, 85, 93 ]

## 堆排序的时间复杂度

最坏时间复杂度	 O(n log n)

最优时间复杂度	 O(n log n)