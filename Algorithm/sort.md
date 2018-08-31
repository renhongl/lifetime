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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjE0MTM1MDU5MF19
-->