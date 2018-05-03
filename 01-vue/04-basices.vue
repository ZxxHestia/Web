<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Vue基础3</title>
	<script type="text/javascript" src="vue.min.js"></script>
</head>
<body>
	<div id="app">
		<!--  -->
		<ol>
			<todo-item v-for="item in sites" :todo="item"></todo-item>
		</ol>
<!-- 自定义事件 -->
		<p>{{totle}}</p>
		<button-count v-on:increment-totle="incrementTotle"></button-count>
		<button-count v-on:increment-totle="incrementTotle"></button-count>

	</div>


	<script type="text/javascript">
		Vue.component('todo-item',{
			props:['todo'],
			template:'<li>{{todo.text}}</li>'
		})
		Vue.component('button-count',{
			template:'<div>'+
						'<button v-on:click="incrementHandle(0)">-</button>'+
						'{{count}}'+
						'<button v-on:click="incrementHandle(1)">+</button>'+
					'</div>',
			data:function(){
				return  {
					count:0
				}
			},
			methods:{
				incrementHandle:function(v){
					if(v==0){
						this.count-=1
						this.$emit('increment-totle',[0])
					}else{
						this.count+=1
						this.$emit('increment-totle',[1])
					}
				}
			}
					
		})
		var vm=new Vue({
			el:'#app',
			data:{
				sites:[
					{text:'jj'},
					{text:'gg'},
					{text:'mm'}
				],
				totle:0
			},
			methods:{
				incrementTotle:function(v){
					if(v==0){
						this.totle-=1
					}else{
						this.totle+=1
					}
				}
			}
		})


	</script>
</body>
</html>