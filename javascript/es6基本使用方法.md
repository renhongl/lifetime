

### 变量声明

1. 使用let和const


### 解构赋值

1. 对对象解构赋值：`const { status, value } = this.props;`


### 字符串的扩展
1. 判断字符串中有字符串`'falskdjflkd'.includes('ab')//false`
2. 字符串中有变量引用，就使用模板字符串：`fjlafdjflajfas${this.props.value}`


### 数字的扩展
1. 使用`Number.isNaN()`判断数字是不是NaN
2. 使用`Number.parseInt(5.22)`将小数转换成整数,parseInt是去掉小数部分。//5
3. 使用 `Math.floor(5.22)`将小数向下取整。//5
4. 使用`Math.ceil(5.22)`将小数向上取整。//6
5. 使用`6.432432.toFixed(2)`将小数取固定位数，返回字符串。//'6.43'

### 函数的扩展
1. 使用参数默认值
		
		function log(x, y = 'World') {
		  console.log(x, y);
		}

2. 使用rest参数

		function add(...values) {
		  let sum = 0;

		  for (var val of values) {
		    sum += val;
		  }

		  return sum;
		}

		add(2, 5, 3) // 10

3. 使用箭头函数


### 数组的扩展

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzMTMyMzcyMSwtMjE0NjMxMTk0MCwxMj
EwODQxMDcxXX0=
-->