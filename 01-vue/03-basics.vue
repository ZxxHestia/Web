<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Vue基础2</title>
	<script type="text/javascript" src="vue.min.js"></script>
<style type="text/css">
		.active{
	width:50px;
	height:50px;
	background:green;
	}
	.text-danger{
		background: red;
	}
</style>
</head>
<body>

	<div id="app">
		<!-- computed setter -->
		<h2>1.computed setter</h2>
		<p>{{ site }}</p>
		<!-- 监听事件 -->
		<h2>2.监听事件</h2>
		千米:<input type="text" v-model="kilometers">
		米:<input type="text" v-model="meters">
		<p id="info"></p>
		<!-- 动态绑定 -->
		<div v-bind:class="{ active: isActive }"></div><br>
		<!-- <div class=" active text-danger"></div> -->
		<div  v-bind:class="{active :isActive,'text-danger':hasError}">多个样式</div>
		<!-- 绑定一个对象 --><br>
		<div v-bind:class="classObject">绑定一个对象</div>
		<!-- 使用计算属性 --><br>
		<div v-bind:class="classObject2">使用计算属性</div>
		<!-- 数组语法 --><br>
		<div v-bind:class="[activeClass,errorClass]">数组语法 </div>
		<!-- 内联样式 -->
		<div v-bind:style="{color:activeColor,fontsize:fontsize+'px'}">内联样式，也可以直接绑定一个对象，数组格式更是可以绑定多个对象</div>
		<!-- 时间处理器 -->
		<p>这个按钮被点击了{{count}}次</p>
		<button v-on:click="count+=1">增加1</button><br>
		<!-- 事件绑定方法 -->
		<button v-on:click="greet">console.log</button><br>
		<!-- 事件传参 -->
		<button v-on:click="say('hi')">Say hi</button>
		<button v-on:click="say('what')">Say what</button><br>
		<!-- 允许点击一次 -->
		<a v-on:click.once="dothis('hi')">dothis</a><br>
		<!-- 监听键盘事件 -->
		<input  v-on:keyup.96="dothis('hi')"><br>
		<!-- 监听按键别名事件 -->
		<input @keyup.a="dothis('hi')">
		<!-- 双向绑定 -->
		<p>textarea 元素:</p>
		<p style="white-space: pre;">{{message2}}</p>
		<textarea v-model="message2" placeholder="请输入多行文本"></textarea><br>
		<!-- 自定义组件 -->
		<global></global>
		<part></part>
		<!-- prop -->
		<child message="hello"></child>
		<!-- 动态prop -->
		<input v-model="parentMsg"><br>
		<child :message="parentMsg"> </child>
	</div>
	<script type="text/javascript">
		var part={
			template:'<h1>自定义组件part!</h1>'
		}

		var vm= new Vue({
			el:'#app',
			data:{
				name1:'jackeyLove',
				name2:'Rookie',
				kilometers:0,
				meters:0,
				isActive:true,
				hasError:true,
				classObject:{
					active:true,
					'text-danger':true
				},
				error:null,
				activeClass:'active',
				errorClass:'text-danger',
				activeColor:'green',
				fontsize:30,
				count:0,
				message2:null,
				age:null,
				parentMsg:'父组件内容'

			},
			methods:{
				greet:function(event){
					console.log('hello'+this.name1+'!')
					if(event){
						console.log(event.target.tagName)
					}
				},
				say:function(message){
					console.log(message)
				},
				dothis:function(message){
					console.log(message)
				}

			},
			//计算属性通过site控制name
			computed:{
				site:{
					get:function(){
						return this.name1+'/'+this.name2+'中下矛盾。'
					},
					set:function(newValue){
						var names=newValue.split(' ')
						this.name1=names[0]
						this.name2=names[1]
					}
				},
				classObject2:function(){
						return{
							active:this.isActive && !this.error,
							'text-danger':this.error &&this.error.type==='fatal'
						}
				}
			},
			watch:{
					kilometers:function(val){
						this.kilometers=val;
						this.meters=val*1000;
					},
					meters:function(val){
						this.kilometers=val/1000;
						this.meters=val;
					}
				},
				components:{
					'part':part
				}
		})

		// 注册全局组件
		Vue.component('global',{
			template:'<h1>自定义组件global!</h1>'
		})
		// 
		Vue.component('child',{
			// 声明 props
			props:['message'],
			// 同样也可以在 vm 实例中像 “this.message” 这样使用
			template:'<span>{{message}}</span>'
		})

		// $watch 是一个实例方法
		vm.$watch('kilometers',function(newValue,oldValue){
			// 这个回调将在 vm.kilometers 改变后调用
			document.getElementById("info").innerHTML="修改前值为:"+oldValue+",修改值后为:"+newValue;
		})
		// 赋予site值
		vm.site='cool uzi';

		vm.greet()
	</script>
</body>
</html>