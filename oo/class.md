

#### 面向对象练习


##### 写一个people类

1. 具有姓名，年龄，性别的属性
2. 具有获取姓名，获取年龄，获取性别的方法
3. 具有设置年龄，设置性别的方法
4. 具有跑步的方法

		class People {
			constructor(name, age, gender) {
				this.name = name;
				this.age = age;
				this.gender = gender;
			}
			
			getName() {
				return this.name;
			}
			
			getAge() {
				return this.age;
			}
			
			getGender() {
				return this.gender;
			}
			
			setAge(age) {
				this.age = age;
			}
			
			setGender(gender) {
				this.gender = gender;
			}
			
			run() {
				console.log('people run');
			}
		}

##### 写一个student类

1. 继承people类
2. 重写跑步方法，student跑得快一些
3. 具有学习的方法

		class Student extends People {
			constructor(name, age, gender) {
				this.name = name;
				this.age = age;
				this.gender = gender;
			}
			
			run() {
				console.log('student run faster');
			}
			
			study() {
				console.log('student study');
			}
		}



##### 写一个student management类

1. 具有查看学生的方法
2. 具有添加学生的方法
3. 具有更新学生的方法
4. 具有删除学生的方法

		class StudentMgmt {
			constructor(list) {
				this.list = list;
			}
			
			getList() {
				return this.list;
			}
			
			addStudent(student) {
				this.list.push(student);
			}
			
			updateStudent(stu) {
				this.list.forEach(student => {
					if (stu.name === student.name) {
						student.age = stu.age;
						student.gender = stu.gender;
					}
				});
			}
			
			deleteStudent(name) {
				let deleteIndex = 0;
				this.list.forEach((student, i) => {
					if (student.name === name) {
						deleteIndex = i;
					}
				});
				this.list.splice(deleteIndex, 1);
			}
		}





**注：** 如果是没有返回值的方法，只用简单的打印字符串即可。
注意方法参数的传递，注意返回值。
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjU1NjM4NjBdfQ==
-->