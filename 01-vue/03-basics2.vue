<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Vue基础2</title>
	<script type="text/javascript" src="vue.min.js"></script>
</head>
<body>

	<div id="app">
		<!-- computed setter -->
		<h2>17.computed setter</h2>
		<p>{{ site }}</p>
	</div>
	<script type="text/javascript">
		var vm= new Vue({
			el:"#app",
			data:{
				name1:'jackeyLove',
				name2:'Rookie'
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
				}
			}
		})
		// 赋予site值
		vm.site='cool uzi';
	</script>
</body>
</html>