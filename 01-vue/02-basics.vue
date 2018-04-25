<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>vue基础</title>
	<script type="text/javascript" src="vue.min.js"></script>
</head>
<style type="text/css">
	.class1{
		background: #444;
		color: #eee;
	}
</style>
<body>
	<div id="app">
		<!-- 添加HTML -->
		<h2>1.添加HTML</h2>
		<div v-html="message"></div>

		<!-- 复选框改变属性值 -->
		<h2>2.复选框改变属性值</h2>
		<label v-bind:class="{'class1':class1}" >改变字体颜色</label>
		<input type="checkbox" v-model="class1" >
		<br><br>

		<!-- 语法表达式 -->
		<h2>3.语法表达式</h2>
		{{5+5}}<br>
		{{ok?'YES':'NO'}}<br>
		{{message.split('').reverse().join('')}}
		<div v-bind:id="'list-'+id">根据属性设置id值</div>

		<!-- if表达式 -->
		<h2>4.if表达式</h2>
		<p v-if="seen">现在你看到我了</p>
		<template v-if="seen2">
			<p>现在你能看到一整块了</p>
			<p>现在你能看到一整块了X2</p>
		</template>

		<!-- v-bind 缩写 : -->
		<h2>5.v-bind 缩写 :</h2>
		<pre><a  v-bind:href="url">我的git项目</a></pre>

		<!-- v-model根据当前值改变属性值 -->
		<h2>6.v-model根据当前值改变属性值</h2>
		<p>{{ vm }}</p>
		<input v-model="vm">

		<!-- v-on监听事件 缩写 @ -->
		<h2>7.v-on监听事件 缩写 @</h2>
		<p>{{vo}}</p>
		<button v-on:click="reverseVo">反转字符串</button>

		<!-- 自定义过滤器 -->
		<h2>8.自定义过滤器</h2>
		<p>{{a | doFilter}}</p>
		
		<!-- if ...else-if... else ... -->
		<h2>9.if ...else-if... else ...</h2>
		<div v-if="Math.random()>0.3">
			<p>缘分已到</p>
		</div>
		<div v-else-if="Math.random()>0.5">
			<p>缘分逐渐消失</p>
		</div>
		<div v-else>
			<p>缘分未到</p>
		</div>

		
		<!-- v-show的使用 -->
		<h2>10.v-show的使用</h2>
		<h4 v-show="ok">v-if与v-show的区别？</h4>
		<h4>在切换 v-if 块时，Vue.js 有一个局部编译/卸载过程，因为 v-if 之中的模板也可能包括数据绑定或子组件。v-if 是真实的条件渲染，因为它会确保条件块在切换当中合适地销毁与重建条件块内的事件监听器和子组件。v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——在条件第一次变为真时才开始局部编译（编译会被缓存起来）。相比之下，v-show 简单得多——元素始终被编译并保留，只是简单地基于 CSS 切换。
		一般来说，v-if 有更高的切换消耗而 v-show 有更高的初始渲染消耗。因此，如果需要频繁切换 v-show 较好，如果在运行时条件不大可能改变 v-if 较好。</h4>
		

		<!-- v-for指令 数组遍历-->
		<h2>11.v-for指令 数组遍历</h2>
		<ul>
			<template v-for="site in sites">
				<li>{{site.name}}</li>
			</template>
		</ul>

		<!-- v-for指令2 value-->
		<h2>12.v-for指令2 value</h2>
		<ul>
			<template v-for="value in customer">
				<li>{{value}}</li>
			</template>
		</ul>

		<!-- v-for指令3 key与value-->
		<h2>13.v-for指令3 key与value</h2>
		<ul>
			<template v-for="(value,key) in customer">
				<li>{{key}}:{{value}}</li>
			</template>
		</ul>

		<!-- v-for4  key与value与index-->
		<h2>14.v-for4  key与value与index</h2>
		<ul>
			<template v-for="(value,key,index) in customer">
				<li>{{index+1}}.{{key}}:{{value}}</li>
			</template>
		</ul>

		<!-- v-for5 迭代整数 -->
		<h2>15.v-for5 迭代整数</h2>
		<ul>
			<li v-for="n in 3">
				{{n}}
			</li>
		</ul>

		<!--3楼的字符串反转写在上面不容易理解，计算属性了解一下。  -->
		<h2>16.3楼的字符串反转写在上面不容易理解，计算属性computed 了解一下。</h2>
		<p>计算反转字符串:{{reverseMessage}}</p>
		<h4>computed vs methods</h4>
		<h4>我们可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。</h4>

		

		
		









	</div>

	<script type="text/javascript">
		new Vue({
			el:'#app',
			data:{
				message:'<h1>添加HTML</h1>',
				class1:false,
				ok:true,
				message:'NAZI',
				id:1,
				seen:true,
				seen2:false,
				url:"https://github.com/ZxxHestia/Web",
				vm:"zxx",
				vo:"daxia",
				a:"vvvvv",
				sites:[
					{name:'zxx'},
					{name:'ppd'},
					{name:'777'}
				],
				customer:{
					name:'zxx',
					sex:'男',
					age:'5'
				}

			},
			computed:{
				// 计算属性的getter
				reverseMessage:function(){
					//this指向vue实例
					return this.message.split('').reverse().join('')
				},
				customer:{
					get:function(){
						return this.name+' '+this.sex+' '+this.age
					},
					set:function(newValue){
						this.name=newValue
					}
				}

			},
			// filters只能在method上
			filters:{
					doFilter:function(value){
						if(!value) return ''
						value=value.toString()
						return value.charAt(0).toUpperCase()+value.slice(1)

					}
				},
			methods:{
				reverseVo:function(){
					this.vo=this.vo.split('').reverse().join('')
				}

			}
		})
	</script>
</body>
</html>