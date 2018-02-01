## 扩展运算符

* 好比rest参数的逆运算，将一个数组转换为用逗号分隔的参数序列。

  **所以需要用圆括号装起来：（...[1, 2, 3, 4]）**

* 可以用来替代函数的apply方法:

  ```
  //ES5写法-----apply方法第一个参数是上下文，第二个参数是方法的参数列表，但是是装在同一个数组里面。
  function f(x, y, z) {
    //...
  }
  var args = [0, 1, 2];
  f.apply(null, args);


  //ES6写法
  function f(x, y, z) {
    //...
  }
  let args = [1, 2, 3];
  f(...args);
  ```

* 求数组最大值:

  ```
  //ES5写法
  Math.max.apply(null, [23, 12, 54]);

  //ES6写法
  Math.max((...[23, 12, 54]));
  //等同于求max方法的参数的最大值
  Math.max(23, 12, 54)
  ```

* 将一个数组的所有元素一次添加到另一个数组

  ```
  //ES5写法
  var arr1 = [1, 2, 3];
  var arr2 = [4, 5, 6];
  Array.prototype.push.apply(arr1, ar2);

  //ES6的写法----因为push可以接受若干参数一次添加进数组，如果传入的是一个数组，那么这个数组就被当做整体添加就一个元素了。
  arr1.push(...arr2);
  ```

* 复制数组

  ```
  //ES5写法----concat用于连接两个数组，然后返回一个新数组，那么这两个数组就不是指向同一个地址了。
  const a1 = [1, 3];
  const a2 = a1.concat();

  //ES6写法
  const a1 = [1, 2];
  const a2 = [...a1];//创建了新数组，填入了a1的所有项
  ```

* 合并数组

  ```
  //ES5写法
  [1, 2].concat(more);
  var arr1 = [1, 2];
  var arr2 = [3, 4];
  var arr3 = [5, 6];
  arr1.concat(arr2, arr3);

  //ES6写法
  [1, 2, ...more];
  [...arr1, ...arr2, ...arr3];
  ```

  ​

