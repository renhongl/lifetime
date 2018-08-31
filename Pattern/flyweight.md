  

#### 享元模式

  

享元模式（Flyweight Pattern）主要用于减少创建对象的数量，以减少内存占用和提高性能。这种类型的设计模式属于结构型模式，它提供了减少对象数量从而改善应用所需的对象结构的方式。

  

享元模式尝试重用现有的同类对象，如果未找到匹配的对象，则创建新对象。

  

* 例子：

  

		class Flyweight{
			constructor() {
				this.divPool = [];
			}

			createDiv(text, parent) {
				if (this.divPool.length > 0) {
					console.log(`get from pool, pool count:${this.divPool.length}`);
					let div = this.divPool.shift();
					div.innerText = text;
					parent.appendChild(div);
					return div;
				} else {
					console.log(`create a new div, because pool count:${this.divPool.length}`);
					let div = document.createElement('div');
					div.innerText = text;
					parent.appendChild(div);
					return div;
				}
			}
		  
			removeDiv(node, parent) {
				parent.removeChild(node);
				this.recover(node);
				console.log(`when ui remove div, restore this div, now pool has: ${this.divPool.length}`);
			}
		  
			recover(node) {
				this.divPool.push(node);
			}
		}
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEzNTkwNTIxOV19
-->