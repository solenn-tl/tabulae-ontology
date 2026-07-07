# Scénario de motivation du modelet Sources

## Nom

Sources

## Description

Le modelet Sources a pour objectif de faire le lien entre les informations décrites dans le graphe de connaissances et les sources dont elles sont issues.

Une source possède deux principales formes : 
* concept/idée générale : contenu de la source considéré indépendement de sa forme concrète;
* forme concrète, qui peut être :
    * physique : exemplaire physique d'un document, généralement caractérisé par un identifiant et une localisation ;
    * numérique : version numérisée d'un document physique, base de donnée, inventaire d'archive ... ;
    * dérivée : version obtenue suite à un traitement automatique ou manuel (ex: plan géoréférencé, page transcrite...) d'une source physique/numérique. Il peut y avoir plusieurs formes dérivées d'une même source.

Une source peut être scindée en plusieurs parties qui peuvent elles-mêmes êtres divisées en éléments documentaires cohérents (ex: registre contient plusieurs pages qui contiennent plusieurs zones).

Une **source** peut être décrite par les propriétés suivantes :
* {*obligatoire*} son **titre ou intitulé**;
* {*obligatoire*} son **type** (ex: plan parcellaire, plan d'assemblage, état de section, matrice, folio, référentiel géographique...)
* {*optionnel*} son **précision de son type** (ex: plan issu d'atlas, plan minute, plan révisé etc.)
* {*optionnel*} son **auteur** (personne physique ou morale)
* {*optionnel*} sa **date de création**
* {*optionnel*} sa **date de début de validité**
* {*optionnel*} sa **date de fin de validité**
* {*optionnel*} sa **description**
* {*si folio, obligatoire*} son **numéro de folio**
* {*si folio, optionnel*} son/ses **numéros de folios alternatifs**
* {*si folio, optionnel*} le **numéro d'un folio équivalent** dans une autre matrice (précédente, suivante,bâtie)
* {si archive physique ou numérisée:*obligatoire*} sa **cote d'archive**
* {physique: *optionnel*} sa **localisation géographique**
* {physique, numérique: *optionnel*} ses **dimensions** 
* {source numérique: *optionnel*} son **URL**
* {archive numérisée: *optionnel*} ses **coordonnées dans l'image**
* {archive numérisé: *optionnel*} son **ordre dans une image**
* {archive numérisée: *optionnel*} sa **résolution**
* {archive numérisée: *optionnel*} son **URL IIIF**
* {archive numérisée,dérivée:*obligatoire*} sa **licence de diffusion**
* {dérivée: *obligatoire*} son **processus de création** 
(ex: géoréférencement, vectorisation, transcription)
* {dérivée: *optionnel*} son **DOI**

## Exemples

### Exemple 1 : Formes de sources
- Une matrice cadastrale comprend une liste alphabétique des propriétaires. Cette liste est un ensemble de pages composées de colonnes qui contiennent de multiples mentions de propriétaires.
- Un exemplaire papier de la matrice est conservée dans un service d'archives et est identifiée par une cote. 
- Chaque page a été numérisée et possède une cote. 
- Les éléments contenus dans chaque page sont détectés et transcrits avec un modèle (DAN).

### Exemple 2
>Exemple de description de l'état de sections primitifs de Marolles en Brie dans ses différentes formes.

#### [Concept]

* **Intitulé** : Etat de sections de Marolles-en-Brie
* **Type** : état de sections 
* **Date de création** : 1810
* **Précision du type** : registre primitif produit avant 1822

#### [Source physique]

* **Intitulé** : Etat de sections de Marolles-en-Brie
* **Type** : état de sections 
* **Date de création** : 1810
* **Précision du type** : registre primitif produit avant 1822
* **Cote d'archive** : 3 P 387
* **Localisation** : Archives départementales du Val-de-Marne

#### [Source numérisée]

* **Intitulé** : Etat de sections numérisé de Marolles-en-Brie
* **Type** : état de sections 
* **Précision du type** : registre primitif produit avant 1822
* **Date de création** : 1810
* **Cote d'archive** : FRAD094_3P_000387_01
* **Licence** : Etalab

#### [Source dérivée]

* **Intitulé** : Dataset contenant la transcription de l'état de sections Marolles en Brie
* **Type** : transcription structurée
* **Date de création** : novembre et décembre 2023
* **Processus de création** : annotation manuelle avec Callico

### Exemple 3

> Exemple de description du plan parcellaire de la section C de Marolles en Brie dans ses différentes formes

#### [Concept]

* **Intitulé** : Plan parcellaire de la Section C "dite du Village" Marolles-en-Brie
* **Type** : plan parcellaire
* **Date de création** : 1810

#### [Source physique]

* **Intitulé** : Plan parcellaire de la Section C "dite du Village" Marolles-en-Brie
* **Type** : plan parcellaire
* **Précision du type** : plan extrait d'un atlas
* **Date de création** : 1810
* **Cote d'archive** : 3 P 1197
* **Localisation** : Archives départementales du Val-de-Marne

#### [Source numérisée]

* **Intitulé** : Plan parcellaire numérisé de la Section C "dite du Village" Marolles-en-Brie
* **Type** : plan parcellaire
* **Précision du type** : plan extrait d'un atlas
* **Date de création** : 1810
* **Cote d'archive** : FRAD094_3P_001197_01
* **Licence** : Etalab

#### [Source dérivée]

* **Intitulé** : Plan parcellaire vectorisé de la section C de Marolles en Brie
* **Type** : plan vectorisé
* **Date de création** : mai 2023
* **Processus de création** : annotation manuelle avec QGIS