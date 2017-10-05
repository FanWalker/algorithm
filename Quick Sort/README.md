# 快速排序

快速排序是一种分而治之思想在排序算法上的典型应用：将原问题分解为若干个规模更小但结构与原问题相似的子问题。递归地解这些子问题，然后将这

些子问题的解组合为原问题的解。

实现原理：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数

据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

## 快速排序算法流程

1、从数列中挑出一个元素，称为 “基准”（pivot）;

2、重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，

该基准就处于数列的中间位置。这个称为分区（partition）操作；

3、对"基准"左边和右边的两个子集，不断重复第一步和第二步，直到所有子集只剩下一个元素为止。

## 动图演示：
![](https://sort.hust.cc/res/quickSort.gif)


## 实例分析：

无序数组array = [85, 24, 63, 45, 17, 31, 96, 50]为例，

第一步：选择中间的元素45作为"基准"。（基准值可以任意选择，但是选择中间的值比较容易理解。）；

[85, 24, 63, **45**, 17, 31, 96, 50]

第二步：按照顺序，将每个元素与"基准"进行比较，形成两个子集，一个"小于45"，另一个"大于等于45"；

[24 17 31] **45** [85 63 96 50]

第三步：对两个子集不断重复第一步和第二步，直到所有子集只剩下一个元素为止；

[24 **17** 31] 45 [85 **63** 96 50]

**17** [24 31] 45 [50] **63** [85 96]

17 [**24** 31] 45 50 63 [**85** 96]

[17 24 31 45 50 63 85 96]


## JavaScript语言实现

第一种实现：

	var quickSort = function(arr){
		if(arr.length <= 1){
			return arr;
		}
		//选择“基准”（pivot），并将其与原数组分离，在定义两个空数组，用来存放一左一右的两个子集
		var pivotIndex = Math.floor(arr.length / 2);
		var pivot = arr.splice(pivotIndex, 1)[0];
		var left = [];
		var right = [];
		
		//开始遍历数组，小于“基准”的元素放入左边的子集，大于基准的元素放入右边的子集
		for(var i=0; i<arr.length; i++){
			if(arr[i] < pivot){
				left.push(arr[i]);
			}
			else{
				right.push(arr[i])
			}
		}
		return quickSort(left).concat([pivot], quickSort(right));
	}
	
	
	var array = [80, 93, 60, 12, 42, 30, 68, 85, 10];
	var newArr = quickSort(array);
	console.log(newArr); //[ 10, 12, 30, 42, 60, 68, 80, 85, 93 ]

根据分治法加上冒泡以及递归综合起来的一种排序，其时间复杂度依然是跟冒泡一样为O(n^2)

## 第二种，改进算法实现：

1）设置两个变量i、j，排序开始的时候：i=0，j=N-1；

2）以中间的数组元素作为关键数据（可以以任意位置的元素作为关键数据），赋值给key，即key=A[arr.length / 2]；

3）从j开始向前搜索，即由后开始向前搜索(j--)，找到第一个小于key的值A[j]，将A[j]和A[i]互换；

4）从i开始向后搜索，即由前开始向后搜索(i++)，找到第一个大于key的A[i]，将A[i]和A[j]互换；

5）重复第3、4步，直到i=j； (3,4步中，没找到符合条件的值，即3中A[j]不小于key,4中A[i]不大于key的时候改变j、i的值，使得j=j-1，i=i+1，直至找到为

止。找到符合条件的值，进行交换的时候i， j指针位置不变。另外，i==j这一过程一定正好是i+或j-完成的时候，此时令循环结束）。

## 第二种示例：

同样以无序数组array = [85, 24, 63, 45, 17, 31, 96, 50]为例，

初始i=0；j=7；

步骤一：先从j到左搜索小于45的进行交换，找到该值后将j赋予该下标；

步骤二：然后再从i到右搜寻大于45的进行交换：找到该值将i赋予该下标；

直到i与j碰面为止；

具体步骤如下，第一轮执行：

第一趟排序：

排序前：i=0；j=7;[85, 24, 63, 45, 17, 31, 96, 50]

步骤一：从右向左递减找到31下标为5

排序后: i=0,j=5;[85, 24, 63, 31, 17, 45, 96, 50]；

第二趟排序：

排序前：i=0,j=5;[85, 24, 63, 31, 17, 45, 96, 50]；

步骤二后：从左到右递增找到大于45的下标为0的85；

排序后：i=0,j=5;[45, 24, 63, 31, 17, 85, 96, 50]；

第三趟排序：

排序前：i=0,j=5;[45, 24, 63, 31, 17, 85, 96, 50]；

步骤三后：从下标为j=5向左递减找到小于45的下标为4的17；

排序后：i=0,j=4;[17, 24, 63, 31, 45, 85, 96, 50]；

第四趟排序：

排序前：i=0,j=4;[17, 24, 63, 31, 45, 85, 96, 50]；

步骤四后：从下标为i=0向右递增找到大于45的下标为2的63；

排序后：i=2,j=4;[17, 24, 45, 31, 63, 85, 96, 50]；

第五趟排序：

排序前：i=2,j=4;[17, 24, 45, 31, 63, 85, 96, 50]；

步骤五后：从下标为j=4向左递减找到小于45的下标为3的31；

排序后：i=2,j=3;[17, 24, 31, 45, 63, 85, 96, 50]；

到第五趟时候就停止，之后以6为中介将左右数据分开递归第一轮执行顺序，直到左右两侧都剩余一个值为止；

### 代码实现：
	function quickSort(arr){
		if(arr.length<2){
			return arr;
		}
		var current = arguments.callee; //返回正被执行的 Function 对象即quickSort()函数本身
		var left = [],
			right = [],
			middle = [];
	
		var key = Math.floor(arr.length/2),
			start=0,
			end = arr.length-1, 
			keyValue=arr[key];
	
	
		rtl(arr, start, end);  //right to left从右到左找到小于基准元素的元素
	
		function rtl(arr, i, j){
			if(i<j){
				if(arr[j] <= keyValue){
					var temp = arr[j],
						index = j;
						arr[j] = keyValue;
						arr[key] = temp;
						j = key;
						key = index;
						ltr(arr, start, end);
						end = index;  //下一趟从下标为index开始从右往左找到小于基准元素的元素
				}
				else{
					end--;
					rtl(arr, i, end);
				}
			}
		}
		function ltr(arr, i, j){
			if(i<j){
				if(arr[i] > keyValue){
					var temp = arr[i],
						index = i;
					arr[i] = keyValue;
					arr[key] = temp;
					i = key;
					key = index;
					rtl(arr, start, end)
					start = index;  //下一趟从下标为index开始从左往右找到大于基准元素的元素
				}
				else{
					start++;
					ltr(arr, start, j)
				}
			}
		}
		return [].concat(current(arr.slice(0,key)), arr[key], current(arr.slice(key+1, arr.length)));
		//相当于return [].concat(quickSort(arr.slice(0,key)), arr[key], quickSort(arr.slice(key+1, arr.length)))
	}
	
	var array = [80, 93, 60, 12, 42, 30, 68, 85, 10];
	var newArr = quickSort(array);
	console.log(newArr); //[ 10, 12, 30, 42, 60, 68, 80, 85, 93 ]

### 比较两种方式：

第一种：也就是传统的"快速排序"其实不是真正的快速排序 而是根据分治法加上冒泡以及递归综合起来的一种排序，其时间复杂度依然是跟冒泡一样为O(n^2)
因为每一次分组进行比较都是将关键值跟所有对比一遍，不过优点还是代码优美，容易理解；
第二种：虽然代码看上去稍微复杂一些，不过是应用底层的快速排序思想去实现，其时间复杂度为O(nlogn)-O(n^2)
有关复杂度计算可以参考算法复杂度
也就是说第二种的时间复杂度在最差情况下跟第一种是一样的也是O(n^2)而最好的情况仅仅是O(nlogn)


### 学习参考：

[真正的快速排序算法javascript实现](http://blog.csdn.net/u012545279/article/details/17412665) *by玉超*

[快速排序（Quicksort）的Javascript实现](http://www.ruanyifeng.com/blog/2011/04/quicksort_in_javascript.html)*阮一峰的网络日志*


