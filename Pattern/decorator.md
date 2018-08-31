

 **例子：**

	//Example 1
	Function.prototype.before = function(beforeFn) {
	    let self = this;
	    return function() {
	        beforeFn.apply(this, arguments);
	        self.apply(this, arguments);
	    }
	}

	Function.prototype.after = function(afterFn) {
	    let self = this;
	    return function() {
	        self.apply(this, arguments);
	        afterFn.apply(this, arguments);
	    }
	}


	//Example 2
	let a = function() {
	    alert(1);
	}

	let _a = a;

	a = function() {
	    _a();
	    alert(2);
	}

	//Example 3
	window.onload = function() {
	    alert(1);
	}

	let onload = window.onload;

	window.onload = function() {
	    onload();
	    alert(2);
	}

























<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1MjE2MDgxNV19
-->