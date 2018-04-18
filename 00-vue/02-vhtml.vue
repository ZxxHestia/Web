<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>vhtml</title>
	<script type="text/javascript" src="https://cdn.bootcss.com/vue/2.4.2/vue.min.js"></script>
</head>
<body>
	<div id="app">
		<div v-html="message"></div>
	</div>

	<script type="text/javascript">
		new Vue({
			el:'#app',
			data:{
				message:'<h1>zxx小侠</h1>'
			}
		})
	</script>
</body>
</html>