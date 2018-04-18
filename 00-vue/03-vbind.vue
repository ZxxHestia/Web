<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>vbind</title>
	<script type="text/javascript" src="https://cdn.bootcss.com/vue/2.4.2/vue.min.js"></script>
</head>
<style type="text/css">
	.class1{
		background: #444;
		color: #eee;
	}
</style>
<body>
	<div id="app">
		<!-- v-bind绑定class1 -->
		<label v-bind:class="{'class1':class1}" >改变字体颜色</label>
		<!-- v-model动态改变class1 -->
		<input type="checkbox" v-model="class1" >
		<br><br>
	</div>

	<script type="text/javascript">
		new Vue({
			el:'#app',
			data:{
				class1:false
			}
		})
	</script>
</body>
</html>