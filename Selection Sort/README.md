# 选择排序

无论什么数据用选择排序算法排序，它的时间复杂度都是O(n²)。



## 选择排序算法流程

1、在未排序序列中找到最小（大）元素，存放到排序序列的起始位置；

2、从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾；

3、重复第二步，直到所有元素均排序完毕。

## 动图演示：

![](https://sort.hust.cc/res/selectionSort.gif)


## JavaScript语言实现
	function SelectionSort(arr){
		var len = arr.length,
			temp,
			minIndex;
		for(var i=0; i< len-1; i++){
			minIndex = i;
			for(var j=i+1; j<len; j++){
				if(arr[j]<arr[minIndex]){
					minIndex = j;
				}
			}
			temp = arr[minIndex];
			arr[minIndex] = arr[i];
			arr[i] = temp;
	
		}
		return arr;
	}
	var array = [8, 5, 2, 6, 9, 3, 1, 4, 0, 7];
	var newArr = SelectionSort(array);
	console.log(newArr);  //[ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

## 选择排序的时间复杂度

O(n²)