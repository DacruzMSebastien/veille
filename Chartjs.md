# Chart.js

###  Introduction
Chart.js est une bibliothèque JavaScript open source représentant des données sous forme de graphiques.
 
###  Création de l'environnement de travail
Créons un nouveau répertoire dans lequel nous allons créer un fichier index.html et chart.js

### Intégration
 On utilise le CDN que l'on va ajouter en-dessous des balises meta du fichier index.html
`<script  src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.7.2/Chart.js"></script>`

Ensuite, entre les balises body nous allons créer une balise canvas.
Exemple : `<canvas  id="myChart"></canvas>`

Enfin, sous la balise de fermeture body, ajoutons le lien vers notre fichier JavaScript précédemment créé.
`<script  src="chart.js"></script>`

### Création du graphique
Tout ce qui va suivre est à c/c dans le fichier chart.js

**On sélectionne notre canvas via le DOM**

`var  ctx  =  document.getElementById("myChart");`

**On instancie le graphique en précisant son type**.
Pour cet exemple, il s'agira d'un graphique en barres. Il existe 9 catégories différentes :
bar, line, pole area, doughnut, bubble, scatter, area, mixed
`var  myChart  =  new  Chart(ctx, {`
`type:  'bar',`

**Vient ensuite les données du graphique** 
```
data: {
	labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
	datasets: [{
		label:  '# of Votes',
		data: [12, 19, 3, 5, 2, 3],
```

"labels" correspond aux noms donnés sur l'axe des abscisses (x)
"label" est le titre donné au graphique
"data" sont les données de l'axe des ordonées (y)
Ainsi, "Red" vaut 12, "Blue" vaut 19, etc.

**Toujours dans datasets, on va donner une couleur pour chaque élément de l'abscisse**
```
backgroundColor: [
	
	'rgba(255, 99, 132, 0.2)',
	'rgba(54, 162, 235, 0.2)',
	'rgba(255, 206, 86, 0.2)',
	'rgba(75, 192, 192, 0.2)',
	'rgba(153, 102, 255, 0.2)',
	'rgba(255, 159, 64, 0.2)'

],
borderColor: [
	'rgba(255,99,132,1)',
	'rgba(54, 162, 235, 1)',
	'rgba(255, 206, 86, 1)',
	'rgba(75, 192, 192, 1)',
	'rgba(153, 102, 255, 1)',
	'rgba(255, 159, 64, 1)'
],
borderWidth:  1
}]
```
Voilà pour les couleurs, c'est assez explicite, à noter que borderWidth correspond à l'épaisseur de la bordure. 1 est la valeur de base et 0 supprime la bordure


**Enfin, pour que l'axe des ordonnées commence bien à 0**

On insère la valeur "scales" dans les options du graphique.
```
 },
options: {
	scales: {
		yAxes: [{
			ticks: {
				beginAtZero:true
			}
		}]
	}
}
});
```


**Le code complet ;** 
```
var  ctx  =  document.getElementById("myChart");
var  myChart  =  new  Chart(ctx, {
	type:  'bar',
	data: {

		labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
		datasets: [{
		label:  '# of Votes',
		data: [12, 19, 3, 5, 2, 3],
		
		backgroundColor: [
			'rgba(255, 99, 132, 0.2)',
			'rgba(54, 162, 235, 0.2)',
			'rgba(255, 206, 86, 0.2)',
			'rgba(75, 192, 192, 0.2)',
			'rgba(153, 102, 255, 0.2)',
			'rgba(255, 159, 64, 0.2)'
		],

		borderColor: [
			'rgba(255,99,132,1)',
			'rgba(54, 162, 235, 1)',
			'rgba(255, 206, 86, 1)',
			'rgba(75, 192, 192, 1)',
			'rgba(153, 102, 255, 1)',
			'rgba(255, 159, 64, 1)'
		],
		borderWidth:  1
		}]
	},
	options: {
		scales: {
			yAxes: [{
				ticks: {
					beginAtZero:true
				}
			}]
		}
	}
});
```
-----
-----
Ceci constitue un graphique **en barres** tout à fait basique. Le code change selon la catégorie de graphique que l'on va utiliser mais globalement, on retrouvera toujours ce même "template".

 Aussi, il existe un tas de fonctionnalités supplémentaires. Je vous conseille de regarder la [documentation](https://www.chartjs.org/) - qui est dailleurs très bien faite - pour vous en apercevoir.
 Pour vous donner une idée de ce que l'on peut faire, on va ajouter une petite animation.
 
 **Dans les options du graphique, à l'instar de scales, nous allons écrire :**
 ```
 animation: {
	duration:  3000,
	easing:  'easeInOutQuint'
}
```
"duration" correspond à la durée, en milliseconde.
Ici, j'ai choisi "easeInOutQuint" mais il en existe une pléthore. 
Voici le [lien](https://www.chartjs.org/docs/latest/configuration/animations.html) de toutes les animations disponibles.

Cela donne ça;
 ```
options: {
	scales: {
		yAxes: [{
			ticks: {
				beginAtZero:true
			}
		}]
	},
	animation: {
		duration:  3000,
		easing:  'easeInOutQuint'
		}
	}
});
```

### Exercice

Dans le cadre du Hacktion Commando, j'ai été amené à travailler avec une enterprise (Desimone) où j'ai eu recours à Chart.js
Voici un des exercices que j'ai dû réaliser:

Créer un graphique en barres (horinzontale) où en orordonnées sont affichées les heures (sur 24h à interval de 15mn) et en abscisse les valeurs des différentes consommations électriques des éléments. 

Voici les valeurs qui doivent figurer sur le graphique  (j'ai réadapté l'exercice pour que cela soit plus simple et surtout beauuuucoup moins long que ce qui m'était demandé).

type: 'horizontalBar'

label: "Consommation Groupe Froid" affichée en bleu

labels: 10h, 12h, 14h, 16h, 18h (ordonnées)

data: 648.00, 672.00, 650.00, 648.00, 672.00 (abscisse)

----
----
---
----
**Hint**

Concrètement, les données devraient se présenter comme cela:
 ```
 type: '',
 data: {
	labels: [],
	datasets: [{
			label:
			backgroundColor:
			data:
		}]
}`;



