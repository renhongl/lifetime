#### 观察者模式

**具体写法：** 使用Map将话题和要执行的回调方法一一对应的存下来，即订阅。在发布这个话题时，使用发布的参数，执行这个话题的回调方法。

**订阅前发布：** 在发布某个话题时，如果这个话题尚未被订阅，那么将这个话题存储起来，等订阅之后，立即发布。那么，在写代码时，就不会发生发布在订阅之前，导致功能不能被触发的问题。

**命名空间：** 如果整个项目都使用了此模式，很容易在没有命名空间的情况下混淆话题。

**例子：**

	class Observer{
		constructor() {
			this.topicMapping = {};
			this.publishStore = {};
		}	  

		subscribe(...args) {
			let topic = args.shift();
			let callback = args.shift();
			if (!this.topicMapping[topic]) {
				this.topicMapping[topic] = [];
			}
			this.topicMapping[topic].push(callback);
			console.log(`subscribed topic ${topic}`);
			//check if had subscribed
			if (this.publishStore[topic]) {
				console.log(`trigger topic ${topic} immediately`);
				this.publish(topic, this.publishStore[topic]);
				delete this.publishStore[topic];
			}
		}
	  
		publish(...args) {
			let topic = args.shift();
			if (this.topicMapping[topic]) {
				this.topicMapping[topic].forEach((v, k) => {
					v.apply(null, args);
				});
			} else {
				console.log(`no topic: ${topic} has been subscribed, this publish will store here, after subscribe, will trigger`);
				this.publishStore[topic] = args;
			}
		}
	  
		unsubscribe(...args) {
			let topic = args.shift();
			let callback = args.shift();
			if (this.topicMapping[topic]) {
				delete this.topicMapping[topic];
				if (callback instanceof Function) {
					callback(args);
				}
			} else {
			console.log(`no topic ${topic} has been subscribe, so no need unsubscribe.`);
			}
		}
	}
	export default Observer;
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4Mjc2NzM3XX0=
-->