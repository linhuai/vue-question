# vue 的 methods 属性、计算属性(computed)、watch 属性的区别
------
## 1、methods 属性和计算属性的区别
　　我们可以将同一个函数定义为一个方法页不是计算属性。而两种方法的最终结果确实是完全相同的。然而，不同的是**计算属性是基于它们的依赖进行缓存的**。计算属性只有在它们的相关依赖发生改变时才会重新计算值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。


## 2、 计算属性(computed)和侦听函数(watch) 的区别
　　watch 有两个参数 新/旧值，计算属性没有，但是可以从 setter 获得新值

	//html
	<div id="demo">{{ fullName }}</div>

	//js | 使用 watch 属性实现
	var vm = new Vue({
		el: '#demo',
		data: {
			firstName: 'Foo',
			lastName: 'Bar',
			fullName: 'Foo Bar'
		},
		watch: {
			firstName: function ( val ) {
				this.fullName = val + ' ' + this.lastName;
			},
			lastName: function ( val ) {
				this.fullName = this.firstName + ' ' + val;
			}
		}
	})

		// js | 使用 computed 属性实现
		var vm = new Vue({
			el: '#demo',
			data: {
				firstName: 'Foo',
				lastName: 'Bar'
			},
			computed: {
				fullName () {
					return this.firstName + ' ' + this.lastName;
				}
			}
		})

**总结：**

1、当有一些数据需要随着其他数据的变动而变动时，使用 computed / watch

2、当需要在数据变化时执行异步操作或开销较大的操作时，使用watch

3、重新计算开销很大的话请选择计算属性

4、不希望有缓存的请用 methods 性性
