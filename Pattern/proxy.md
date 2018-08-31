### 代理模式

代理模式是为一个对象提供一个代用品或占位符，以便控制对它的访问。

代理和本体接口保持一致，那么用户可以放心的请求代理，他只关心是否得到想要的结果；在任何使用本体的地方都可以替换成使用代理。

虚拟代理：例如实现图片预加载、合并http请求。

缓存代理：例如缓存ajax异步请求的数据，下次再打开同一页的时候，便可以直接使用之前的数据。

例子：

```
export class LoadImage{
    setUrl(url, target) {
        target.src = url;
    }
}

export class LoadImageProxy{
    constructor() {
        this.loadImage = new LoadImage();
    }

    setUrl(url, target) {
        this.loadImage.setUrl('./image/p2.gif', target);
        let img = new Image();
        img.onload = () => {
            setTimeout(() => {
                this.loadImage.setUrl(url, target);
            }, 2000);
        }
        img.src = url;
    }
}

export class LoadData{
    constructor() {
        this.data = {
            renhong: {
                name: 'renhongl',
                age: 18
            },
            mogu: {
                name: 'mogu',
                age: 19
            }
        };
    }

    load(name, callback) {
        setTimeout(() => {
            callback(this.data[name]);
        }, 2000);
    }
}

export class LoadDataProxy{
    constructor() {
        this.loadData = new LoadData();
        this.cache = {};
    }

    load(name, callback) {
        if (!this.cache[name]) {
            this.loadData.load(name, (data) => {
                this.cache[name] = data;
                callback(data);
            });
        } else {
            callback(this.cache[name]);
        }
    }
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTA1ODczNTU4XX0=
-->