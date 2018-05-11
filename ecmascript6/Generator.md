## Generator函数

### 基本用法

```
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hwg = helloWorldGenerator();
hwg.next();//{value: 'hello', done: false}
hwg.next();//{value: 'world', done: false}
hwg.next();//{value: 'ending',  done: true}
hwg.nexe();//{value: undefined, done: true}
```



