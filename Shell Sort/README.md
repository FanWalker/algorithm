# 希尔排序

希尔排序算法以其设计者希尔（Donald Shell）的名字命名，是插入排序算法的一种更高效的改进版本。但希尔排序是非稳定排序算法。

希尔排序的基本思想是：先将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序，待整个序列中的记录“基本有序”时，再对全体记录进行以

此直接插入排序。



## 希尔排序算法流程

1、先取一个正整数 d1(d1 < n)，把数列分成d1个组：所有距离为d1的倍数的数列元素分成一组，然后在各组内进行插入排序；

2、然后取 d2(d2 < d1)；

3、重复上述分组和排序操作；直到取 di = 1(i >= 1) 位置，即所有元素成为一个组，最后对这个组进行插入排序。一般选 d1 约为 n/2，d2 为 d1 /2， d3 为 

d2/2 ，…， di = 1。

## 动图演示：

![](http://bubkoo.qiniudn.com/shell-sort-animation.gif)


## 实例分析：

假设有数组 array = [80, 93, 60, 12, 42, 30, 68, 85, 10]，首先取 d1 = 4，将数组分为 4 组，如下图中相同颜色代表一组：

![](http://bubkoo.qiniudn.com/shell-sort-step1.1.png)

然后分别对 4 个小组进行插入排序，排序后的结果为：

![](http://bubkoo.qiniudn.com/shell-sort-step1.2.png)

然后，取 d2 = 2，将原数组分为 2 小组，如下图：

![](http://bubkoo.qiniudn.com/shell-sort-step2.1.png)

然后分别对 2 个小组进行插入排序，排序后的结果为：

![](http://bubkoo.qiniudn.com/shell-sort-step2.2.png)

最后，取 d3 = 1，进行插入排序后得到最终结果：

![](http://bubkoo.qiniudn.com/shell-sort-step3.png)

## JavaScript语言实现
	function ShellSort(arr){
		var len = arr.length,
			gap = Math.floor(len/2);
	
		function swap(arr, i , k){
			var temp = arr[i];
			arr[i] = arr[k];
			arr[k] = temp;
		}
	
		while(gap>0){
			for(var i=gap; i<len; i++){
				while(i>0){
					if(arr[i-gap] > arr[i]){
						swap(arr, i-gap, i);
					}
					else{
						break;
					}
					i -= gap;
				}
			}
			gap = Math.floor(gap/2);
		}
		return arr;
	
	}
	var array = [80, 93, 60, 12, 42, 30, 68, 85, 10];
	var newArr = ShellSort(array);
	console.log(newArr); //[ 10, 12, 30, 42, 60, 68, 80, 85, 93 ]
