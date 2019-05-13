<!DOCTYPE html>
<html>
<head>
	<title>AirStrike</title>
</head>
<body>
	<style type="text/css">
		#ocean {
			background-image: url("img/ocean.jpg");
			width: 900px;
			height: 700px;
		}
		.player {
			position: absolute;
			background-image: url("img/player.png");
			width: 70px;
			height: 75px;
		}
		.enemy {
			position: absolute;
			background-image: url("img/enemy.png");
			width: 70px;
			height: 75px;			
		}
		.missle {
			position: absolute;
			background-color: orange;
			width: 2px;
			height: 10px;
		}
	</style>

	<div id="ocean">
		<div id="players"></div>
		<div id="enemies"></div>
		<div id="missles"></div>
	</div>
	
	<script type="text/javascript">
	
	var player = {
		left: 450,
		top: 620
	}
	var enemies = [
		{left: 250, top: 250}, // left upper corner
		{left: 450, top: 150}, // middle top
		{left: 650, top: 250}, // right upper corner
		{left: 450, top: 250}, // middle center
		{left: 350, top: 300}, // left lower corner
		{left: 550, top: 300}, // right lower corner
		{left: 450, top: 350} // middle bottom
	]
	var missles = []
	function drawPlayer(){
		content = "<div class='player' style='left:"+player.left+"px; top: "+player.top+"px'></div>";
		document.getElementById("players").innerHTML = content;
	}
	function drawEnemies(){
		content = "";
		//console.log(enemies);
		for(var idx=0; idx < enemies.length; idx++){
			content += "<div class='enemy' style='left:"+enemies[idx].left+"px; top:"+enemies[idx].top+"px'></div>";
		}
		//console.log(content);
		document.getElementById("enemies").innerHTML = content;
	}
	function drawMissles(){
		content = "";
		for(var idx=0; idx<missles.length; idx++){
			content += "<div class='missle' style='left:"+missles[idx].left+"px; top:"+missles[idx].top+"px'></div>"
		}
		document.getElementById("missles").innerHTML = content;
	}
	function moveEnemies(){
		for(var idx=0; idx < enemies.length; idx++){
			//console.log(idx);
			enemies[idx].top = enemies[idx].top + 1;			
		}
	}
	function moveMissles(){
		for(var idx=0; idx < missles.length; idx++){
			missles[idx].top = missles[idx].top - 5;
		}
	}
	document.onkeydown = function(e) {
		console.log(e);
		if(e.keyCode == 37 && player.left > 0){ // Left
			player.left = player.left - 10;
		}
		if(e.keyCode == 39 && player.left < 830){ // Right
			player.left = player.left + 10;
		}
		if(e.keyCode == 38 && player.top > 500){ // Up
			player.top = player.top - 10;
		}
		if(e.keyCode == 40 && player.top < 630){ // Down
			player.top = player.top + 10;
		}
		if(e.keyCode == 32){ // Spacebar (fire)
			missles.push({left: (player.left+34), top: (player.top-8)})
			drawMissles();
		}
		console.log(missles);
		drawPlayer();
	}
	function gameLoop(){
		console.log("gameLoop is running");
		drawPlayer();
		moveEnemies();
		drawEnemies();
		moveMissles();
		drawMissles();
		setTimeout(gameLoop, 24);
	}
	gameLoop();
	</script>
</body>
</html>
