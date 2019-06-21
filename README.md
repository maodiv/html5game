#html5
<!DOCTYPE html>
<html>

<meta http-equiv="Content-Type" content="text/html; charset=utf-8">

<head>
<title></title>

	<style>
		body{
			margin:0
		}
	</style>

</head>
<body>
	<style>
		.content{
			width:100%;
			height:100%;
			position:fixed;
		}
	
		.header{
			background-color: black;
			height: 80px;
			width:100%;
		}
		.header h1{
			color:white;
			display:inline-block;
			margin:0px;
		}
		
		.middle{
			width:100%;
			height:auto;
			
		}
	
		.middle_left{
			list-style-type: none;
			background-color: #f1f1f1;
			border-right: 1px solid #ddd;
			
			float: left;
			
			
			height:100%;
			width: 10%;
			padding: 0px;
			margin: 0px;
			
			overflow:auto;
			
		}
		.middle_left li a{
			display:block;
			padding: 6px 8px;
			text-decoration:none;
			color:black;
		}
		.middle_left li a:hover{
			background-color: #555;
			color:white;
		}
		
		.middle_right{
			float: right;
		
			height:100%;
			width: 80%;
			padding: 10px 10px;
			margin: 0px;
			
			overflow:auto;
		}
	</style>

<div class="content">
	<div class="header">
		<h1>系统</h1>
	</div>
	
	<div class="middle">
		<ul class="middle_left">
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>	
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>	
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>	
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>	
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
		<li><a href="#nav1">导航一</a></li>
		<li><a href="#nav2">导航二</a></li>
		<li><a href="#nav3">导航三</a></li>
		<li><a href="#nav4">导航四</a></li>
		<li><a href="#nav5">导航五</a></li>		
	</ul>
		<div class="middle_right">
	  <h2>Fixed Full-height Side Nav</h2>
	  <h3>Try to scroll this area, and see how the sidenav sticks to the page</h3>
	  <p>Notice that this div element has a left margin of 25%. This is because the side navigation is set to 25% width. If you remove the margin, the sidenav will overlay/sit on top of this div.</p>
	  <p>Also notice that we have set overflow:auto to sidenav. This will add a scrollbar when the sidenav is too long (for example if it has over 50 links inside of it).</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <h3>Try to scroll this area, and see how the sidenav sticks to the page</h3>
	  <p>Notice that this div element has a left margin of 25%. This is because the side navigation is set to 25% width. If you remove the margin, the sidenav will overlay/sit on top of this div.</p>
	  <p>Also notice that we have set overflow:auto to sidenav. This will add a scrollbar when the sidenav is too long (for example if it has over 50 links inside of it).</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <h3>Try to scroll this area, and see how the sidenav sticks to the page</h3>
	  <p>Notice that this div element has a left margin of 25%. This is because the side navigation is set to 25% width. If you remove the margin, the sidenav will overlay/sit on top of this div.</p>
	  <p>Also notice that we have set overflow:auto to sidenav. This will add a scrollbar when the sidenav is too long (for example if it has over 50 links inside of it).</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <h3>Try to scroll this area, and see how the sidenav sticks to the page</h3>
	  <p>Notice that this div element has a left margin of 25%. This is because the side navigation is set to 25% width. If you remove the margin, the sidenav will overlay/sit on top of this div.</p>
	  <p>Also notice that we have set overflow:auto to sidenav. This will add a scrollbar when the sidenav is too long (for example if it has over 50 links inside of it).</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <h3>Try to scroll this area, and see how the sidenav sticks to the page</h3>
	  <p>Notice that this div element has a left margin of 25%. This is because the side navigation is set to 25% width. If you remove the margin, the sidenav will overlay/sit on top of this div.</p>
	  <p>Also notice that we have set overflow:auto to sidenav. This will add a scrollbar when the sidenav is too long (for example if it has over 50 links inside of it).</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	  <p>Some text..</p>
	</div>
	</div>

	

</div>

	


</body>
</html>
