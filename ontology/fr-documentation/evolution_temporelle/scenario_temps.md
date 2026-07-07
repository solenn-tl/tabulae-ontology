# Scénario de motivation du modelet Evolution temporelle

## Nom

Evolution des parcelles cadastrales et des comptes fonciers

## Description

1. Evolution des parcelles
2. Evolution des comptes fonciers

### 1. Evolution des parcelles cadastrales

Le premier objectif de ce modelet est de décrire l'évolution des parcelles cadastrales au cours du temps, de leur création à leur disparition à l'échelle de leurs attributs (contribuables, nature, adresse).

En l'absence de plans parcellaires disponibles après la date de création du cadastre, l'évolution des parcelles (existence et attributs) est reconstituée à partir des états de parcelle qui se trouvent dans les comptes fonciers des matrices des contribuables. 
Reconstituer l'évolution de chaque parcelle nécessite de naviguer dans la matrice, de comptes fonciers en comptes fonciers, en utilisant les colonnes de reports de folios (souvent nommées *Tiré de* et *Porté à*). 

Dans le cas général, en France, les descriptions des parcelles sont regroupées par contribuables dans des comptes fonciers, eux-mêmes situés dans les matrices cadastrales. 

### 1.1 Existence de la parcelle

L'identité d'une parcelle, dans une commune donnée, sur le temps long, est définie par le numéro de la parcelle et un même périmètre.

En effet, les numéros de parcelles étaient fixés par le plan cadastral et n'étaient pas amenés à changer jusqu'à l'archivage de celui-ci. 
On considère donc qu'une parcelle existe tant que son périmètre ne change pas. 

Une parcelle **apparaît** : 
* soit à l'**initialisation du cadastre** (à la suite de la levée du plan),
* soit à la suite d'une **division d'une parcelle** de surface supérieure en 2..n parcelles,
* soit après une **fusion de 2..n parcelles**.
Une parcelle **disparait** : 
* soit lors de la **clôture du cadastre** (qui est remplacé par un autre corpus avec une nouvelle numérotation du parcellaire),
* soit à la suite d'une **division d'une parcelle** de surface supérieure en 2..n parcelle,
* soit après une **fusion de 2..n parcelles**.

Si un état de parcelle dans un compte foncier renvoie à plusieurs autres états de parcelles dans des comptes fonciers différents, ont peut considèrer que la parcelle est divisée (les indivisions ayant généralement leur propre compte foncier). 

En cas de division : 
* Le numéro d'une parcelle mère est transmis aux parcelles filles, parfois suivit de la lettre *p* (mais ce n'est pas systématique).
En cas de fusion (cas rare) : 
* soit les parcelles fusionnées portaient le même numéro et c'est ce numéro qui persiste ;
* soit les numéros des différentes parcelles sont collés et forment un nouveau numéro.

Certains évènements sont associés à des changements majeurs de la documentation cadastrale (nouvelle cadastration) ou à des redécoupages des unités administratives (création d'une nouvelle commune ou échanges de territoires entre communes). 
A la suite de ces événements particuliers, le parcellaire peut être complètement remanié et les parcelles renumérotées, ce qui est souvent associé à la création d'un nouveau cadastre.
Dans le cas où une commune possède deux cadastres successifs, il est difficile d'établir documentairement les liens de filiations entre les parcelles d'une version à l'autre. Les tables de correspondances des numéros, quand elles étaient produites, n'ont pas toujours été conservées. 

### 1.2 Evolution des attributs

Une parcelle, pour une année T, est caractérisée par plusieurs attributs: 
* un **contribuable** (ou groupe de contribuable) décrits dans un compte foncier
* une ou plusieurs **natures** de sol (ex: bâtiment et cour)
* une **localisation/adresse** (lieu-dit, voie, section, commune)
* une **géométrie** (dont le périmètre exact n'est connu que pour les parcelles ne subissant aucune fusion ou division depuis la création du cadastre)

Une version d'un attribut correspond à une période de stabilité de sa valeur. Cet état stable peut être attesté par un ou plusieurs états de classement successifs extraits des comptes fonciers dans les matrices. La compilation des états qui attestent de cette stabilité permet d'en déduire les dates de la période de validité.

### 1.3 Résumé : évolution des parcelles
* Une parcelle possède une période d'existance allant de sa création à sa disparition liée à une modification de son périmètre.
* La valeur des attributs des parcelles change au cours du temps. Chaque attribut possède donc plusieurs versions qui ont une période de validité donnée.
* On peut donc distinguer deux catégories d'événements : les événements liés directement à l'identité de la parcelle (apparition, disparition) et les événements liés à ses propriétés.

## 2. Evolution des comptes fonciers

L'évolution temporelle des comptes fonciers se traduit :
* par des entrées et sorties d'états de parcelles (dont l'évolution est décrite plus haut)
* par des entrées et sorties de contribuables qui se transmettent des biens (ventes ou sucessions).

Dans le deuxième cas, l'information mise à jour sont des libellés de contribuables (*voir modelet "Contribuables"*), souvent la date d'entrée du contribuable dans le compte foncier qui correspond à la date de sortie du contribuable précédent. 

Le détail du fonctionnement des comptes fonciers est décrit dans le modelet *Fonctionnement des documents cadastraux*. Ces changements de contribuables doivent être suivis pour pouvoir attacher chaque état de parcelles (valide de T1 à T2) au contribuable responsable à une date Tn.

## 3. Précision temporelle dans le cadastre ancien

La précision temporelle dans le cadastre ancien est de l'ordre de l'année.

Les bornes de l'intervalle de validité d'une propriété peuvent être :
* deux années (ex : <i>1810-1850</i>,<i>1856-1856</i>)
* une année et une intervalle (ex : <i>1810-entre 1832 et 1882</i>,<i>entre 1832 et 1882-1914</i>)
* deux intervalles (ex : <i>entre 1810 et 1812-entre 1832 et 1882</i>,<i>entre 1832 et 1882-1914</i>)

Les intervalles sont données quand il n'est pas posside de fournir une année, en utilisant généralement les dates de création/archivage des registres fournies par les métadonnées d'archives.

## Exemples

### Exemple 1 : Initialisation d'une parcelle

#### Contexte
Les états de sections fournissent l'état initial de la parcelle (dans une version du cadastre donnée). La date associée à cet état est l'année de production de cet état de section. Elle peut être indiquée/récupérée de plusieurs façons :
* extraction depuis la source numérisée
* **indiquée dans les métadonnées de la côte d'archive**

#### Exemple
>Année de production de l'état de sections de Marolles en Brie : *1810*
* Date d'apparition de chaque parcelle (déduite) : 1810
* Borne de début de l'intervalle de validité de l'ensemble des états qui suivent directement celui-ci : 1810

### Exemple 2 : Validité d'une propriété

#### Contexte
L'intervalle de validité d'une propriété est déduite à l'aide des dates des N états sucessifs de la parcelle pour lesquels la propriété conserve la même valeur ainsi qu'à partir de la date d'entrée de l'état N+x pour lequel la valeur de la propriété change.

Ces états sont principalements décrits dans les matrices cadastrales. 

#### Exemple
>Parcelle 191, Section C, Marolles-en-Brie

*1. Sucession d'états*
<table>
    <tr><th>Source <i>(+ num extraction)</i></th>
        <th>Compte foncier</th>
        <th>Propriétaire</th>
        <th>Nature</th>
        <th>Tiré de</th>
        <th>Date d'entrée</th>
        <th>Porté à</th>
        <th>Date de sortie</th>
    </tr>
    <tr>
        <td>Etat de section</td>
        <td></td>
        <td>Mazarot Pierre cabaretier à id</td>
        <td>Jardin</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>Matrice de rôle</td>
        <td>43</td>
        <td>Mazarot Pierre cabaretier,
            D’Auvergne de Noiseau et
            Jn Bt Fleury
        </td>
        <td>Jardin</td>
        <td></td>
        <td></td>
        <td>94</td>
        <td></td>
    </tr>
    <tr>
        <td>Matrice de rôle</td>
        <td>94</td>
        <td>Mazarot Pierre cabaretier à id</td>
        <td>Jardin</td>
        <td>43</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>Matrice des propriétés foncières</td>
        <td>57</td>
        <td>Mazarot Pierre cabaretier à Marolles</td>
        <td>Jardin</td>
        <td></td>
        <td></td>
        <td>45</td>
        <td>1832</td>
    </tr>
    <tr>
        <td>Matrice des propriétés foncières</td>
        <td>45</td>
        <td>Guillot Pierre Louis Victor ainé à</td>
        <td>Jardin</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>

