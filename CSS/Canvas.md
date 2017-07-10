---
title: Canvas Demo
date: 2017-7-6
tags: [canvas demo]
categories: CSS
---
简单的使用canvas
```

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>

	<script type="text/javascript">
	function rectangle(){
		var canvas = document.getElementById('rectangle');
		if(canvas == null) return false;
		var context = canvas.getContext("2d");
		context.fillStyle = "red";
		context.strokeStyle = "blue";
		context.fillRect(0,120,100,100);//x,y,width,height
		context.strokeRect(0,120,100,100);

		context.strokeStyle = "rgba(255,0,0,0.2)";
		context.strokeRect(120,120,100,100);
	}
	function circle(){
		var canvas = document.getElementById('circle');
		if(canvas == null) return false;
		var context = canvas.getContext('2d');
		context.beginPath();
		context.strokeStyle = "blue";
		context.moveTo(100,100); //将路径的起点设置为圆心，闭合的时候才会闭合圆心
		context.lineTo(200,100); //这句话写不写都没事
		context.stroke();	
		context.arc(100, 100, 100,0, 1.5*Math.PI,true);
		//圆心（100,100），半径100，起始角0，结束角1.5PI，逆时针
		//默认为false顺时针，true为逆时针，最右边为0*Math.PI，顺时针依次是0.5*Math.PI,1*Math.PI,1.5*Math.PI,
		context.closePath();
		context.fillStyle = 'rgba(0,255,0,0.25)';//默认是黑色
		context.fill(); //闭合的时候会找起点闭合，从而达到四分之一圆的效果

	}
	function line(){
		  var canvas = document.getElementById('line');
            if (canvas == null)
                return false;
            var context = canvas.getContext("2d");
            context.beginPath();
            context.strokeStyle = "rgb(250,0,0)"; //和stroke()相对应
            context.fillStyle = "rgb(250,0,0)" //和fill()相对应
            //实验证明第一次lineTo的时候和moveTo功能一样，选择起点
            context.lineTo(50, 100);
            //之后的lineTo会以上次lineTo的节点为开始，作为终点
            context.lineTo(100, 100);
            context.stroke();
            context.closePath();
            context.beginPath(); //一定要有，不然第一条绘制的路径也会被绘制成第二个颜色
            context.moveTo(100, 150);
            context.lineTo(200,150);
            context.strokeStyle = "rgb(0,250,0)";
            context.stroke();
            context.closePath();
	}
	window.onload = function(){
		rectangle();
		circle();
		line();
	}
	</script>
</head>
<body>
	<section>
		<canvas id="rectangle" width="400px" height="400px"></canvas>
	</section>
	<section>
		<canvas id="circle" width="400px" height="400px"></canvas>
	</section>
	<section>
		<canvas id="line" width="400px" height="400px"></canvas>
	</section>
</body>
</html>

```
参考：http://www.cnblogs.com/tim-li/archive/2012/08/06/2580252.html#top
