  
  

#### 命令模式

  

命令模式（Command Pattern）是一种数据驱动的设计模式，它属于行为型模式。请求以命令的形式包裹在对象中，并传给调用对象。

调用对象寻找可以处理该命令的合适的对象，并把该命令传给相应的对象，该对象执行命令。

  
  

* 例子：

  

		class RenderLogin{
		constructor() {
		this.login = document.createElement('div');
		this.options = {
		width: '100px',
		height: '100px',
		border: '1px solid red'
		}
		}

		render(options) {
		this.options = {...this.options, ...options};

		for (let key of Object.keys(this.options)) {

		this.login.style[key] = this.options[key];

		}

		document.body.appendChild(this.login);

		}

		  

		remove() {

		document.body.removeChild(this.login);

		}

		}

		  

		class RenderLoginCommand{

		constructor() {

		this.renderLogin = new RenderLogin();

		}

		  

		excute(reciever) {

		this.renderLogin.render(reciever.options);

		}

		  

		undo() {

		this.renderLogin.remove();

		}

		}

		  

		export class LoginButton{

		constructor() {

		this.options = {

		background: 'grey',

		borderRadius: '50%'

		}

		this.renderLoginCommand = new RenderLoginCommand();

		}

		}
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY3NDA1MTgyM119
-->