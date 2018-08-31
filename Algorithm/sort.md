#### 排序

##### 快速排序

	/**
	* 快速排序
	* 取第一个值，作为中间值，与余下的一次比较
	* 比中间值小的，放左边数组
	* 比中间值大的，放右边数组
	* 递归调用，直到每个数组只剩一个元素，返回该数组
	*/
	export  const quickSort = (arr) => {
		if(arr.length <=1){
			return arr
		}
		let mid = arr[0];
		let left =[];
		let right =[];
		for (let i =1; i<arr.length; i++){
			if(arr[i]<mid){
				left.push(arr[i]);
			}else{
				right.push(arr[i]);
			}
		}
		return quickSort(left).concat([mid],quickSort(right));
	}

##### 冒泡排序

	/**

* 冒泡排序

* 取前一个和后一个值比较，前者大则交换

* 第一次循环结束，最后一个值为最大

* 数组有多长，外层循环多少次

*/

export  const bubbleSort = (arr) => {

for (let i = arr.length - 1; i >=0; i--) {

for (let j = 0; j < i; j++) {

if (arr[j] > arr[j+1]) {

let temp = arr[j];

arr[j] = arr[j+1];

arr[j+1] = temp;

}

}

}

return arr;

}
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ2NDY3NTAwMywyMTQxMzUwNTkwXX0=
-->