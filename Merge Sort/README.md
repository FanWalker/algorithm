# 归并排序

归并排序是建立在归并操作上的一种有效的排序算法，该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。它是一种稳定的排序算法

其原理：将两个已经排序的序列合并成一个序列的操作。

归并排序的实现有两种方法：

（1）自上而下的递归；（2）自下而上的迭代

## 归并排序算法流程

1、把n个记录看成n个长度为1的有序子表；

2、进行两两归并并使记录关键字有序，得到n/2个长度为2的有序子表；

3、再将得到的有序子表又进行两两合并排序；

4、重复第三步骤直到所有记录归并成一个长度为 n 的有序表为止。

## 动图演示：
![](https://sort.hust.cc/res/mergeSort.gif)


## 实例分析：

无序数组array = [6, 5, 3, 1, 8, 7, 2, 4]为例，

第一步：原始状态[6, 5, 3, 1, 8, 7, 2, 4]；

第二步：将数组分为长度为2的子数组并两两合并排序[5 6] [1 3] [7 8] [2, 4]；

第三步：继续两两合并排序[1, 3, 5, 6]  [2, 4, 7, 8]；

第四步：重复第三步：[1, 2, 3, 4, 5, 6, 7, 8]，最后得到的结果就为[1, 2, 3, 4, 5, 6, 7, 8]。

## JavaScript语言实现
	function merge(left,right){
		var result = [];
	
		while(left.length && right.length){
			if(left[0]<right[0]){
				result.push(left.shift());
			}
			else{
				result.push(right.shift());
			}
		}
		return result.concat(left, right);
	
	}
	
	function mergeSort(a){
		if(a.length === 1){
			return a;
		}
		var work = [],
			len = a.length;
	
		for(var i=0; i<len; i++){
			work.push([a[i]]);
		}
		work.push([]); //因为在数组长度为奇数，会出错，这里应该再push一个空数组，避免出错
	
		for(var lim = len; lim > 1; lim = ~~((lim + 1) / 2)){   //~~替代 Math.floor(),~~在性能上来说更快 。
			for(var j=0, k=0; k < lim; j++, k+=2){
				work[j] = merge(work[k], work[k + 1]);
			}
			work[j] = [];  //作用同上
		}
		return work[0];
	}
	
	var array = [80, 93, 60, 12, 42, 30, 68, 85, 10];
	var newArr = mergeSort(array);
	console.log(newArr); //[ 10, 12, 30, 42, 60, 68, 80, 85, 93 ]
