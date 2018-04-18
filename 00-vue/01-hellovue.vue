<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Vue第一个页面</title>
	<script src="https://cdn.bootcss.com/vue/2.4.2/vue.min.js"></script>
</head>
<body>
	<div id="vue_det">
		<h1>site:{{site}}</h1>
		<h1>author:{{author}}</h1>
		<h1>mobile:{{mobile()}}</h1>
	</div>
	<script type="text/javascript">
		var vm=new Vue({
			el:'#vue_det',
			data:{
				site:"第一个vue页面",
				author:"zxx"
			},
			methods:{
				mobile:function(){
					return "18613131313";
				}
			}
		})
		document.write(vm.a===data.a)
	</script>
</body>
</html>