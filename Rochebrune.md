title       : Généricité pour la gestion et la valorisation des données scientifiques
subtitle    : l'apport des métadonnées
author      : Julien Barde, Wilfried Heintz
date: "2016-01-18"
job         : UMR MARBEC, IRD, Sète & UMR DYNAFOR, INRA, Toulouse
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      #   
widgets     : [bootstrap, quiz]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
license     : by-nc-sa
github:
  user: jsubei
  repo: IRDTunaAtlas
logo        : logo_IRD.svg
knit        : slidify::knit2slides
ext_widgets : {rCharts: ["libraries/highcharts","libraries/nvd3", "libraries/morris", "libraries/leaflet", "libraries/rickshaw"]}
---
# Donnée ou métadonnée ?

Une donnée non décrite est-elle utilisable ?

Niveau 0 : Valeurs brutes + intitulés de colonnes non explicites

Id | Es. |	Dia |	H |	Enc.
--------|--------|--------|--------|--------
3.1 | FS | 76 | 15,5 | 80
3.2 | FS | 69 | 16,3 | 80
3.3 | FS | 66 | NA | 80
3.4 | FS | 47 | NA | 80
3.5 | FS | 21 | NA | 80
3.6 | QP | 52 | 18,4 | 80
3.7 | FS | 18 | 15,6 | 80
3.8 | QP | 16 | 10,1 | 80


---
# Donnée ou métadonnée ?

Peut-on parler de donnée si elle n'est pas exploitable ?

Niveau 1 : Valeurs brutes + intitulés de colonnes explicites 

Identifiant de l'arbre| Espèce | Diamètre à 1m30 (cm) |  Hauteur (m) |	% encombrement de la canopée
--------|--------|--------|--------|--------
3.1 | FS | 76 | 15,5 | 80
3.2 | FS | 69 | 16,3 | 80
3.3 | FS | 66 | NA | 80
3.4 | FS | 47 | NA | 80
3.5 | FS | 21 | NA | 80
3.6 | QP | 52 | 18,4 | 80
3.7 | FS | 18 | 15,6 | 80
3.8 | QP | 16 | 10,1 | 80


---
# Donnée ou métadonnée ?

Donnée exploitable = données brutes + métadonnées

Niveau 2 : Valeurs brutes + intitulés de colonnes explicites + contexte

<fieldset><b>Identification des arbres de la zone 1 - 10/04/2015</b> <br/><br/>
FS : Fagus sylvatica <br/><br/>
QP : Quercus pubescens <br/><br/>
<b>Heure de début</b> : 10h30 - <b>Heure de fin</b> : 12h30		<br/><br/>
<b>Lieudit</b> : "Courrade"		<br/><br/>
<b>Type</b> : accru de feuillus mélangés  	<br/><br/>
<b>Système de référence utilisé</b> : WGS84/UTM 31	<br/><br/>
<b>Coordonnées GPS station de référence</b> : X=4768605 Y=274434  	<br/><br/>
<b>Contact</b> : lb@toulouse.inra.fr</fieldset>


---
# (Méta)donnée

Où finit la donnée ? Où commence la métadonnée ? 

La séparation est arbitraire et dépend du format et de la nature de la donnée :
 
 - la métadonnée est embarquée (jpeg, NetCDF)
 - la métadonnée est séparée (shp)
 
On peut écrire une partie des métadonnées avant de créer la donnée !
  

---
# Pourquoi des métadonnées ?

Décrire une ressource (donnée, information, connaissance) pour informer d'autres personnes :
 - sur l'existence, la pertinence et l'origine d'une ressource :
  - data discovery
  - data relevance
  - data lineage
 - sur l'utilisation correcte de la ressource :
  - métadonnées d'usage (dictionnaire de données),


---
# Pourquoi des métadonnées ?

Décrire une ressource (donnée, information, connaissance, traitement) pour informer d'autres personnes :
 - sur les services liés à la ressource :
  - data access,
  - data processing


---
# Pourquoi des métadonnées ?

Décrire une ressource (donnée, information, connaissance, traitement) pour garantir :

 - un archivage pérenne
 - l'interopérabilité pour la réutilisation par d'autres communautés d'utilisateurs.


---
# Pourquoi des métadonnées ?


<br/>
<center> <span style="font-size:40px;color:red;"><b>Pas de métadonnée => perte de donnée.</b></span></center>
 


---
# Impopularité des métadonnées

Produire des métadonnées est souvent perçu comme une contrainte.

Les - :
- exercice chronophage et complexe,
- rarement effectué par le producteur,
- réalisé "pour les autres" : altruisme <i>sensus stricto</i>,
- multitude de formats et d'outils : choix et implémentation difficiles.


---
# Impopularité des métadonnées

Mais c'est une activité qui peut s'avérer rentable

Les + :
- écrire la métadonnée une fois prend moins de temps qu'en parler n fois,
- compréhension, interopérabilité, <u>pérennité</u>, accessibilité,
- étape indispensable pour l'obtention de DOI & datapaper,
- standards éprouvés et outils actuels ergonomiques.


---
# Métadonnées découvertes

Fournir des métriques pour permettre aux utilisateurs d'en estimer l'intérêt :
- Où ? étendue spatiale,
- Quand ? étendue temporelle,
- Quoi ? composition spécifique,
- Quoi ?  traits / caractéristiques observés,
- Indicateurs : exemple de ressources produites à partir de la donnée brute.

---