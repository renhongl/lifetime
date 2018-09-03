
#### 查找

##### 二分查找

	  
  

	/**
	* 二分查找
	* 将要查找的值与中间值比较
	* 如果比中间值小，寻找范围的结束下标从最后一个值的下标变为中间值的下标减一
	* 反之，将寻找范围的开始下标从第一个值的下标变为中间值加一
	* 直到找到中间值，或者开始下标大于结束下标为止
	*/

	export  const binarySearch = (arr, key) => {
		let begin = 0;
		let end = arr.length - 1;
		while(begin <= end) {
			let middle = begin + Number.parseInt((end - begin)/2);
			if (arr[middle] < key) {
				begin = middle + 1;
			} else  if (arr[middle] > key) {
				end = middle - 1;
			} else {
				return middle;
			}
		}
		return -1;
	}
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDU1MzkwMjgxXX0=
-->