# simongame

<!doctype html>
<html lang="fr">
<head>
<meta charset="utf-8">
<title>Jeu du Simon</title>
<script>
window.onload = function() {
	function ordi() {
		//Tirage d'une couleur au hasard
		let j = Math.round(Math.random()*(colors.length-1));
		color = colors[j];
		displayedColors.push(color);
			
		let iNextColor = 0;
		
		//Affichage toute les couleurs une par une
		let minuterie = window.setInterval(function(){
			
			if(iNextColor < displayedColors.length) {
				//zone.style.backgroundColor = 
				let selectedColor = displayedColors[iNextColor++];	//'green'
				let square = document.getElementById(selectedColor);
				
				square.style.opacity = 0.25;
				
				let resetSquare = window.setTimeout(function() {
					square.style.opacity = 1;
				}, 500);
				
				console.log(displayedColors[iNextColor-1]);
			} else {
				window.clearInterval(minuterie);
			}
		}, 1000);
	}

	function resetGame() {
		displayedColors = [];
		score = 0;
		curseur = 0;
		finJeu = false;
	}
	
	let colors = ['yellow','blue','red','green'];
	let displayedColors = [];
	let color;
	let zone = document.getElementById('zone');
	let score = 0;
	let finJeu = false;
	
	ordi();
	
	let squares = document.getElementsByClassName('square');
	let choice;
	let curseur = 0;
	
	for(let i=0;i<squares.length;i++) {
		squares[i].onclick = function() {
			choice = this.id;
			
			//Vérifier si la couleur cliquée est correcte
			if(choice == displayedColors[curseur++]) {
				console.log('ok');
			} else {
				console.log('GAME OVER!');
				if(confirm('Votre score est de '+score+' points.\nVoulez-vous recommencer?')) {
					resetGame();
					ordi();
				} else {
					finJeu = true;
					
					alert('Appuyez sur SPACE pour recommencer');
					window.onkeydown = function(e) {
						if(finJeu && e.keyCode==32) {
							resetGame();
							ordi();
						}
					};
				}
			}
			
			//Changement de tour
			if(!finJeu && curseur == displayedColors.length) {
				console.log('Tour suivant');
				curseur = 0;
				score += displayedColors.length*0.5;
				console.log(score);
				ordi();	
			}
		};
	}
	
	
};
</script>
<style>
section {
	border: 5px solid silver;
	text-align: center;
}

div#row1,div#row2 {
	width: 100%;
	height: 100%;
	
}

div#row1 div,div#row2 div {
	display: inline-block;
}

div {
	width: 250px;
	height: 250px;
	
}

div#green {
	background-color: green;
}

div#red {
	background-color: red;
}

div#blue {
	background-color: blue;
}

div#yellow {
	background-color: yellow;
}
</style>
</head>
<body>
<section id="zone">
	<div id="row1">
		<div id="green" class="square"></div>
		<div id="red" class="square"></div>
	</div>
	<div id="row2">
		<div id="blue" class="square"></div>
		<div id="yellow" class="square"></div>
	</div>
</section>
</body>
</html>
