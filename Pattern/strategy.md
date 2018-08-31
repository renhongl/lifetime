### 策略模式

定义一系列的算法，把它们一个个封装起来，并且使它们可以互相替换。

一个基于策略模式的程序至少由两部分组成。第一个部分是一组策略类，策略类封装了具体的算法，并负责具体的计算过程。第二个部分是环境类context，context接受客户的请求，随后把请求委托给某一个策略类。

策略模式可以消除程序中大片的条件分支语句。

```
class LevelA{
    calculate(salary) {
        return salary * 2;
    }
}

class LevelB{
    calculate(salary) {
        return salary * 3;
    }
}

class LevelC{
    calculate(salary) {
        return salary * 4;
    }
}

export class GetBonus{
    constructor() {
        this.calculateMapping = {
            A: new LevelA(),
            B: new LevelB(),
            C: new LevelC()
        }
    }

    calculate(type, salary) {
        return this.calculateMapping[type].calculate(salary);
    }
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM2NjM2MzY0MV19
-->