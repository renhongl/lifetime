### 单例模式

保证一个类仅有一个实例，并提供一个访问它的全局访问点。

推荐使用惰性单例的方式创建，即在需要时才创建单例对象。并且需要把不变的部分隔离出来，把管理单例的逻辑和创建对象的逻辑分开，这两个方法可以独立变化而不互相影响。当它们连接在一起时，就完成了创建唯一实例对象的功能。

**例子：**

```
//以下是基本实现方法，但是并没有实现：
//并且需要把不变的部分隔离出来，把管理单例的逻辑和创建对象的逻辑分开
//这两个方法可以独立变化而不互相影响。当它们连接在一起时，就完成了创建唯一实例对象的功能。"
//的功能。因为再加一个单例元素时，需要修改管理单利的类。SingletonDOM只是为CreateDOM而生的管理类。

export class SingletonDOM{
    constructor() {
        this.createDOM = new CreateDOM;
    }

    create() {
        if (!this.instance) {
            return this.instance = this.createDOM.create();
        }
        return this.instance;
    }
}

export class CreateDOM{
    create(type) {
        return document.createElement(type || 'div');
    }
}

export class CreateButton{
    create() {
        return document.createElement('button');
    }
}

//通用管理单例的类。

export class GetSingleton{
    constructor(ClassName) {
        this.obj = new ClassName();
    }

    create() {
        if (!this.instance) {
            return this.instance = this.obj.create();
        }
        return this.instance;
    }
}

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDYwODAzMDA1LDE1NzQ5NTQ2MzZdfQ==
-->