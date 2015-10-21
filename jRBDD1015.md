---
title       : Mise en place d'un SPARQL EndPoint
subtitle    : Servir du RDF via HTTP avec Jena & Fuseki
author      : Julien Barde & Wilfried Heintz
date        : October 21, 2015
job         : jRBDD_2015
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      #   
widgets     : [bootstrap, quiz]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
license     : by-nc-sa
logo        : rbdd.png
knit        : slidify::knit2slides
ext_widgets : {rCharts: [libraries/nvd3]}


--- 

## Introduction

  <h3>Des outils <b>génériques</b> pour servir et partager ses données</h3>

Réutilisation des travaux de Julien Barde, UMR IRD Marbec

 - Décrire toutes les ressources d'une unité de Recherche :
 
    - agents, publications, bases de données, images ...
    
 - S'appuyer sur des standards pour diffuser ce patrimoine
 
    - OGC ? EML ? <b>Open-data </b>!
    

--- 

## Introduction

<iframe src = "http://5stardata.info/en/"  onload="this.width=window.innerWidth;this.height=window.innerHeight;"></iframe>


--- 

## Introduction

<iframe src = "http://data.gouv.fr"  onload="this.width=window.innerWidth;this.height=window.innerHeight;"></iframe>


--- 

## Points abordés

 - Présentation de l'outil Jena
 - Pré-requis et préparation du serveur
 - RDFizer les métadonnées ou les données
 - Installation de Fuseki
 - Exemples d'exploitation du Sparql Endpoint


--- 
<img style="position: absolute; top: 10px; right: 10px; border: 1px;" src="assets/img/apache_jena.png">
## Présentation de Jena

  <h3><u>Un Framework pour le Web sémantique</u></h3>
  <h4><i>Source : http://jena.apache.org</i></h4>

Composé de différentes APIs pour implémenter et servir du RDF :

 - API RDF : `noyau du framework`
    - API Sparql : interroger et mettre à jour du RDF avec SPARQL
    - API Ontology : intégrer des modèles `OWL` dans Jena
 - API Store pour `stocker les données`
 - Serveur <b>Fuseki</b> pour représenter du `RDF` et exécuter des `requêtes SPARQL` via `HTTP`


--- 

## Présentation de Jena

<img style="position: absolute; top: 130px; middle: 0; border: 0" src="assets/img/jena_arch1.png">
<img style="position: absolute; top: 430px; middle: 10px; border: 0" src="assets/img/jena_arch2.png">


---
<img style="position: absolute; top: 10px; right: 10px; border: 0; width:300px;" src="assets/img/Apache.gif">
##  Pourquoi Fuseki ?


   - Projet de la `fondation Apache`
      - Open-source
      - Communauté importante de développeurs (HP)
      - Expérience reconnue
   - Déploiement dans Tomcat
   - Persistance des données
   - 3e génération du logiciel
 

---
<img style="position: absolute; top: 10px; right: 10px; border: 0; width:300px;" src="assets/img/ubuntu.png">
##  Pré-requis indispensables


  <h3>Machine connectée + Java + Tomcat</h3>

 - Exemple avec un serveur Linux Ubuntu
 - Port 8080 ouvert
 - Droits d'administration



---
##  Préparation de la machine

  <h3>Installation de Java</h3>
  <h4><i>Source : https://wolfpaulus.com/journal/software/tomcat-jessie </i></h4>

    # java -version
    # su root
    # echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" 
      > /etc/apt/sources.list.d/webupd8team-java.list
    # echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" 
      > /etc/apt/sources.list.d/webupd8team-java.list
    # apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
    # apt-get update
    # apt-get install oracle-javax-installer




---
##  Préparation de la machine

  <h3>Installation de Java</h3>

Pour changer la version de java :

    # update-alternatives --config java


---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Création d'un utilisateur <b>Tomcat</b> :

    # sudo adduser \
        --system \
        --shell /bin/bash \
        --gecos 'Tomcat Java Servlet and JSP engine' \
        --group \
        --disabled-password \
        --home /home/tomcat \
        tomcat


---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Installation des paquets :

    # mkdir -p ~/tmp
    # cd ~/tmp
    # wget http://www.us.apache.org/dist/tomcat/tomcat-8/v8.0.28/bin/apache-tomcat-8.0.28.tar.gz
    # tar xvzf ./apache-tomcat-8.0.28.tar.gz
    # rm ./apache-tomcat-8.0.28.tar.gz

    # sudo mkdir -p /usr/share/tomcat8
    # sudo mv ~/tmp/apache-tomcat-8.0.28 /usr/share/tomcat8

---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Paramétrages :

    # sudo rm -f /usr/share/tomcat
    # sudo ln -s /usr/share/tomcat8/apache-tomcat-8.0.28 /usr/share/tomcat
    
    # sudo chown -R tomcat:tomcat /usr/share/tomcat8
    # sudo chmod +x /usr/share/tomcat/bin/*.sh


---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Changer le port d'écoute (si nécessaire) :

    # sudo nano /usr/share/tomcat8/apache-tomcat-8.0.28/conf/server.xml

    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />


---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Modifier la taille autorisée pour les fichiers WAR :

    # sudo nano /usr/share/tomcat8/apache-tomcat-8.0.28/webapps/manager/WEB-INF/web.xml

      <multipart-config>
        <!-- 50MB max -->
        <max-file-size>52428800</max-file-size>
        <max-request-size>52428800</max-request-size>
        <file-size-threshold>0</file-size-threshold>
      </multipart-config>

---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Créer un rôle manager :

    # sudo nano /usr/share/tomcat8/apache-tomcat-8.0.28/conf/tomcat-users.xml

      <role rolename="tomcat"/>
      <role rolename="manager-gui"/>
      <user username="user" password="mdp" roles="tomcat,manager-gui"/>


---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Démarrer/arrêter le service :

    # sudo /bin/su - tomcat -c /usr/share/tomcat/bin/startup.sh
    # sudo /bin/su - tomcat -c /usr/share/tomcat/bin/shutdown.sh


---
##  Préparation de la machine
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:200px;" src="assets/img/tomcat.png">
  <h3>Installation de Tomcat</h3>

Optimiser le démarrage :

    # nano /usr/share/tomcat8/apache-tomcat-8.0.28/bin/catalina.sh

Ajouter au début du fichier la ligne :

    JAVA_OPTS="-Djava.security.egd=file:/dev/urandom"
    


---
##  Tomcat est opérationnel

<img style="position: absolute; top: 150px; middle; border: 0; width:600px;" src="assets/img/accueil_tomcat.png">


---
##  Démarrage de Fuseki

  <h3>Déploiement du fichier WAR</h3>

    # cd ~/tmp
    # tar xvzf apache-tomcat-8.0.28.tar.gz
    # rm apache-tomcat-8.0.28.tar.gz
    # sudo cp fuseki.war /usr/share/tomcat8/apache-tomcat-8.0.28/webapps/fuseki.war
    
Puis démarrer Tomcat :

    # sudo /bin/su - tomcat -c /usr/share/tomcat/bin/startup.sh


---
##  Générer du RDF
<img style="position: absolute; top: 20px; right: 30px; border: 0; width:128px;" src="assets/img/rdf.png">
  <h3>RDFization / Triplification (Agents et bibliographies)</h3>

- Convertir une liste d'agents stockée dans un tableau CSV en triplets RDF

- Créer un lien entre ces agents et leur productions scientifiques
  
-> https://github.com/juldebar/RDFization_Foaf_Biblio




---
##  Installation de Fuseki

  <h3>Préparation</h3>

Arrêter Tomcat :

    # sudo /bin/su - tomcat -c /usr/share/tomcat/bin/shutdown.sh

Puis télécharger Fuseki :

    # cd ~/tmp
    # wget http://archive.apache.org/dist/jena/binaries/apache-jena-fuseki-2.3.0.tar.gz
  

---
##  Installation de Fuseki

  <h3>Préparation</h3>

Créer un répertoire pour Fuseki :

    # sudo mkdir /etc/fuseki
    # sudo chown tomcat:tomcat /etc/fuseki

Puis pour le stockage des données :

    # sudo mkdir /data/fuseki
    # sudo chown tomcat:tomcat  /data/fuseki
    

---
##  Installation de Fuseki

  <h3>Copie des données</h3>

Créer un répertoire pour Fuseki :

    # sudo cp ~/tmp/xxx /data/fuseki
    



---
##  Installation de Fuseki

  <h3>Configuration</h3>

Editer le fichier <b>etc/fuseki/config.ttl</b> :

    # Licensed under the terms of http://www.apache.org/licenses/LICENSE-2.0

    ## Fuseki Server configuration file.

    @prefix :        <#> .
    @prefix fuseki:  <http://jena.apache.org/fuseki#> .
    @prefix rdf:     <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs:    <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tdb:     <http://jena.hpl.hp.com/2008/tdb#> .
    @prefix ja:      <http://jena.hpl.hp.com/2005/11/Assembler#> .

    [] rdf:type fuseki:Server ;


---
##  Installation de Fuseki

  <h3>Configuration</h3>

Déclaration d'un service, après la ligne <b># End triples.</b> :

    # Déclaration d'un service
     fuseki:services (
      <#nom_du_service>
     ).



---
##  Installation de Fuseki

  <h3>Configuration</h3>

Description du service :

    # Description du service déclaré prédédemment
     <#nom_du_service> rdf:type fuseki:Service ;
     fuseki:name                       "nom_du_service" ;       # http://host:port/ds
     fuseki:serviceQuery               "sparql" ;   # SPARQL query service
     fuseki:serviceQuery               "query" ;    # SPARQL query service (alt name)
     fuseki:serviceUpdate              "update" ;   # SPARQL update service
     fuseki:serviceUpload              "upload" ;   # Non-SPARQL upload service
     fuseki:serviceReadWriteGraphStore "data" ;     # SPARQL Graph store protocol (read and write)
    # A separate read-only graph store endpoint:
     fuseki:serviceReadGraphStore      "get" ;      # SPARQL Graph store protocol (read only)
     fuseki:dataset                   <#nom_du_dataset> ;
     .


---
##  Installation de Fuseki

  <h3>Configuration</h3>

Description du dataset (mode "mémoire") :

    # Description du dataset déclaré dans le service ci-dessus

     <#nom_du_dataset>   rdf:type ja:RDFDataset ;
     rdfs:label "label_du_dataset" ;
     ja:defaultGraph

---
##  Installation de Fuseki

  <h3>Configuration</h3>


      [ rdfs:label "label_du_graph" ;
        a ja:MemoryModel ;
     ja:content [ja:externalContent <file:/data/fuseki/main.owl> ] ;
     ja:content [ja:externalContent <file:/data/fuseki/resources_def.owl> ] ;
     ja:content [ja:externalContent <file:/data/fuseki/resources.owl> ] ;
     ja:content [ja:externalContent <file:/data/fuseki/foaf_kb_compliant.rdf> ] ;
     ja:content [ja:externalContent <file:/data/fuseki/agents.owl> ] ;
       ] ;
     .

---
##  Installation de Fuseki

  <h3>Sécurité</h3>


Affichage des datasets dans un serveur en ligne (non localhost)

Editer le fichier <b>etc/fuseki/shiro.ini</b> :

     [users]
      # Implicitly adds "iniRealm =  org.apache.shiro.realm.text.IniRealm"
      admin=pw

     [roles]



---
##  Installation de Fuseki

  <h3>Sécurité</h3>

     [urls]
      ## Control functions open to anyone
      /$/status = anon
      /$/ping   = anon

      ## and the rest are restricted to localhost.
      ## /$/** = localhost
      /$/** = authcBasic,user[admin]

---
##  Démonstration en ligne

http://localhost:8080/fuseki

<iframe src = "http://147.99.107.5:8080/fuseki"  onload="this.width=window.innerWidth;this.height=window.innerHeight;"></iframe>

---
##  Inspire et RDF

<iframe src = "http://inspire.data.gouv.fr"  onload="this.width=window.innerWidth;this.height=window.innerHeight;"></iframe>


