---
title       : Mise en place d'un SPARQL EndPoint
subtitle    : Servir du RDF via HTTP avec Jena & Fuseki
author      : Julien Barde & Wilfried Heintz
date        : October 21, 2015
job         : UMR 1201 Dynafor, INRA, Toulouse
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      #   
widgets     : [bootstrap, quiz]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
license     : by-nc-sa
logo        : Dynafor.jpg
knit        : slidify::knit2slides
ext_widgets : {rCharts: [libraries/nvd3]}

--- 
<img style="position: absolute; top: 10px; right: 10px; border: 1px;" src="assets/img/apache_jena.png">
## Présentation de Jena
<h3><u>Un Framework pour le Web sémantique</u></h3>

Composé de différentes APIs pour implémenter et servir du RDF :

 - API RDF : `noyau du framework`
    - API Sparql : interroger et mettre à jour du RDF avec SPARQL
    - API Ontology : intégrer des modèles `OWL` dans Jena
 - API Store pour `stocker les données`
 - Serveur <b>Fuseki</b> pour représenter du `RDF` et exécuter des `requêtes SPARQL` via `HTTP`
 
<i>Source : http://jena.apache.org</i>

---
<img style="position: absolute; top: 10px; right: 10px; border: 0; width:300px;" src="assets/img/Apache.gif">
##  Pourquoi Fuseki ?

 - Projet de la `fondation Apache`
    - Open-source
    - Communauté importante de développeurs
    - Expérience reconnue
 - Déploiement dans Tomcat
 - Persistance des données gérées
 

---
##  Pré-requis indispensables

<h3>Machine connectée + Java + Tomcat </h3>

 - Exemple avec un serveur Linux Ubuntu
 - Port 8080 ouvert
 - Droits d'administration



---
##  Préparation de la machine

<h3>Installation de Java</h3>

Vérification préliminaire :

    - $ java -version

Puis :

    - $ su root
    - $ echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" 
    > /etc/apt/sources.list.d/webupd8team-java.list
    - $ echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" 
    > /etc/apt/sources.list.d/webupd8team-java.list
    - $ apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
    - $ apt-get update
    - $ apt-get install oracle-java`x`-installer



<i>Source : https://wolfpaulus.com/journal/software/tomcat-jessie </i>


---
##  Préparation de la machine

<h3>Installation de Java</h3>

Pour changer de version de java :

$ update-alternatives --config java

<iframe src = "http://147.99.107.5:8080/fuseki/"  onload="this.width=window.innerWidth;this.height=window.innerHeight;"></iframe>

