# Schéma représentants le modelet "Fonctionnement des documents cadastraux"

## 1. Mentions d'une parcelle dans des comptes fonciers
* Le schéma illustre les valeurs associées aux mentions précédentes, courantes et suivantes d'une parcelle dans un compte foncier. Des valeurs spéciales associées à une parcelle au fil du temps peuvent également apparaître.
* Si la cellule associée à la colonne "Tiré de" est vide, la valeur de la propriété ```tbl:takenFrom``` est ```spval:CelluleVide``` par défaut.
* Si la cellule associée à la colonne "Tiré de" est vide, la valeur de la propriété ```tbl:passedTo``` est ```spval:CelluleVide``` est vide par défaut. 
* Pour une représentation fine, complète, de la source, les comptes fonciers (sous-parties de folios qui sont eux-mêmes des sous-parties de pages), doivent avoir été reconnus. Dans le cas contraire, on peut associer des entités correspondant à des folios (```srctype:Folio```) aux propriétés ```tbl:takenFrom``` et  ```tbl:passedTo```.
* Dans cet exemple, on décrit un attribut **d'un objet de type ```peg:Landmark```** possédant un attribut spécifique (```tblatype:PlotMention```) qui permet de retracer son parcours dans les documents. Comme les autres attributs d'instances de ```peg:Landmark``` , ces éléments peuvent être associés à des changements (```peg:Change```) qui sont eux mêmes associés à des évènements (```peg:Event```).

*Pour des questions de lisibilité, seuls les changements entre les deux versions d'attributs sont représentés. Pour obtenir un graphe complet, il faut également représenter les changements liés à l'apparition de la première version d'attribut et à la disparition de la deuxième version d'attributs.*

```mermaid
graph
    %% Class
    Landmark["Parcelle C-347, Commune d'Ablon"]
    LandmarkType(("tblltype:Plot"))
    AttribueClass((peg:Attribute))
    AttributeMen((" "))
    AttributeMenType(("tblatype:PlotMention"))
    AttributeVersion1((" "))
    AttributeVersion2((" "))
    Folio1-5["Compte foncier 1, Folio 5, Matrice de rôles (1817 à 1822)<br><small>a rico:Instantiation"]
    CelluleVide11(("spval:CelluleVide"))
    Folio2-5-2["Compte foncier 2, Folio 5, Matrice des propriétés foncières (1822-1914)<br><small>a rico:Instantiation"]
    Folio3-34-1["Compte foncier 1, Folio 34, Matrice des propriétés foncières (1822-1914)<br><small>a rico:Instantiation"]
    %% Change1((" <br><small>a peg:Change</small>"))
    Change2(("Changement 2 <br><small>a peg:Change</small>"))
    Change3(("Changement 3 <br><small>a peg:Change</small>"))
    %% Change4((" <br><small>a peg:Change</small>"))
    %% Event1(("Evènement<br><small>a peg:Event</small>"))
    Event2(("Evènement 2<br><small>a peg:Event</small>"))
    %% Event3(("Evènement<br><small>a peg:Event</small>"))
    TimeEvent2["1822^^xsd:datetime"]
    Event2Type(("tbletype:DocumentTransition<br><small>a tbl:EventType</small>"))

    %% Relations
    Landmark == peg:isLandmakType ==> LandmarkType
    Landmark == peg:hasAttribute ==> AttributeMen
    AttributeMen == rdf:type ==> AttribueClass
    AttributeMen == peg:isAttributeType ==> AttributeMenType
    %% Change1 == peg:isAppliedTo ==> AttributeMen
    Change2 == peg:isAppliedTo ==> AttributeMen
    Change3 == peg:isAppliedTo ==> AttributeMen
    %% Change4 == peg:isAppliedTo ==> AttributeMen
    %% Change1 == peg:dependsOn ==> Event1
    Change2 == peg:dependsOn ==> Event2
    Change3 == peg:dependsOn ==> Event2
    %% Change4 == peg:dependsOn ==> Event3
    %% Change1 == peg:makesEffective ==> AttributeVersion1
    Change2 == peg:outdates ==> AttributeVersion1
    Change3 == peg:makesEffective ==> AttributeVersion2
    %% Change4 == peg:outdates ==> AttributeVersion2

    Event2 == peg:hasTime ==> TimeEvent2
    Event2 == tbl:isEventType ==> Event2Type

    AttributeMen == peg:hasAttributeVersion ==> AttributeVersion1
    AttributeVersion1 == tbl:isMentionnedIn ==> Folio1-5
    AttributeVersion1 == tbl:takenFrom ==> CelluleVide11
    AttributeVersion1 == tbl:passedTo ==> Folio2-5-2

    AttributeMen == peg:hasAttributeVersion ==> AttributeVersion2
    AttributeVersion2 == tbl:isMentionnedIn ==> Folio2-5-2
    AttributeVersion2 == tbl:takenFrom ==> Folio1-5
    AttributeVersion2 == tbl:passedTo ==> Folio3-34-1

    %% Style

    %% Class -> Style

```

#### Extraits de documents relatifs au schéma
* Version d'attribut n°1 : Compte foncier 1, Folio 5, Matrice de rôles (1817 à 1822)
![Folio 5](./img/ablon_C347_att1.jpg "Archives Départementales du Val-de-Marne, 3P 18")
* Version d'attribut n°2 : Compte foncier 2, Folio 5, Matrice des propriétés foncières (1822-1914)
![Folio 5](./img/ablon_C347_att2.jpg "Archives Départementales du Val-de-Marne, 3P 19")
* 3ème compte foncier dans lequel la parcelle est ajoutée (valeur indiquée par la propriété *tbl:passedTo* )
![Folio 34](./img/ablon_C347_att3.jpg "Archives Départementales du Val-de-Marne, 3P 19")

## 2. Contribuables dans les comptes fonciers
* Le premier exemple illustre les mentions d'une parcelle' dans des comptes fonciers sucessifs.
* Ce second exemple présente l'autre composante importante du fonctionnement des documents cadastraux : les mentions des contribuables dans les comptes fonciers.
* On ne traite pas ici de changements liés à des versions d'attributs de ```peg:Landmark```. Le concept ```peg:Change``` ne peut donc pas être utilisé (voir *domains* et *ranges* définis dans l'ontologie PeGazUs).
* L'ontologie TABULAE introduit le concept de ```tbl:SourceChange``` qui permet de représenter un changement directement lié à un document. Il dépend dans évènement de type ```tbl:SourceEvent``` qui est une sous-classe de ```peg:Event```.

*Pour des raisons de lisibilité, les changements 3  (disparition du 2ème contribuable/apparition du 3ème contribuable) et 4 (disparition du 3ème contribuable) ne sont pas affichés dans la figure.*

```mermaid
graph
    FolioA["Folio 1090<br><small>a rico:Instantiation"]
    FolioSrcType(("srctype:Folio"))
    FolioANum["1090^^Literal"]
    FolioANumAlt["602^^Literal"]
    CFA["Compte Foncier<br><small>a rico:Instantiation</small>"]
    CFASrcType(("srctype:CompteFoncier"))

    Taxpayer1["Macreau Laurent<br><small>a tbl:Taxpayer"]
    Taxpayer2["Bessault Louis<br><small>a tbl:Taxpayer"]
    %%Taxpayer3["Bessault Louis<br><small>a tbl:Taxpayer"]
    
    Change1["Source Change 1<br><small>a tbl:SourceChange</small>"]
    Change2["Source Change 2<br><small>a tbl:SourceChange</small>"]
    %% Change3["Source Change 3<br><small>a tbl:SourceChange</small>"]
    %% Change4["Source Change 3<br><small>a tbl:SourceChange</small>"]

    Change1Type(("tblctype:TaxpayerAppearance"))
    Change2Type(("tblctype:TaxpayerTransition"))
    %%Change3Type(("tblctype:TaxpayerTransition"))
    %%Change4Type(("tblctype:TaxpayerDisappearance"))

    Event1["Source Event 1<br><small>a tbl:SourceEvent</small>"]
    EventTime1Before["1861^^xsd:datetime"]
    EventTime1After["1841^^xsd:datetime"]
    Event1Type((tbletype:OpenPropertyAccount))

    Event2Type((tbletype:TaxpayerMutation))
    Event2["Source Event 2<br><small>a tbl:SourceEvent</small>"]
    Event2Time["1841^^xsd:datetime"]
    Event2Type((tbletype:TaxpayerMutation))

    %%Event3["Source Event 3<br><small>a tbl:SourceEvent</small>"]
    %%Event3Time["1906"^^xsd:date]
    %%Event3Type((tbletype:TaxpayerMutation))
    
    %%Event4["Source Event 3<br><small>a tbl:SourceEvent</small>"]
    %%Event4Time["1906"^^xsd:date]
    %%Event4Type((tbletype:ClosePropertyAccount))

    FolioA == tbl:isSourceType ==> FolioSrcType
    CFA == tbl:isSourceType ==> CFASrcType

    FolioA == rico:hasOrHadComponent ==> CFA
    FolioA == tbl:hasFolioNumber ==> FolioANum
    FolioA == hasAlternativeFolioNumber ==> FolioANumAlt

    %% Mention de contribuables dans un compte foncier
    CFA  == tbl:mentions ==> Taxpayer1
    CFA  == tbl:mentions ==> Taxpayer2
    %%CFA  == tbl:mentions ==> Taxpayer3

    CFA == tbl:sourceChangedBy ==> Change1
    CFA == tbl:sourceChangedBy ==> Change2
    %%CFA == tbl:sourceChangedBy ==> Change3

    Change1 == tbl:sourceChangeDependsOn ==> Event1
    Change1 == tbl:isSourceChangeType ==> Change1Type
    Change1 == tbl:adds ==> Taxpayer1

    Change2 == tbl:sourceChangeDependsOn ==> Event2
    Change2 == tbl:isSourceChangeType ==> Change2Type
    Change2 == tbl:deletes ==> Taxpayer1
    Change2 == tbl:adds ==> Taxpayer2
   
    %%Change3 == tbl:sourceChangeDependsOn ==> Event3
    %%Change3 == tbl:isSourceChangeType ==> Change3Type
    %%Change3 == tbl:deletes ==> Taxpayer2
    %%Change3 == tbl:adds ==> Taxpayer3

    %%Change4 == tbl:sourceChangeDependsOn ==> Event4
    %%Change4 == tbl:isSourceChangeType ==> Change4Type
    %%Change4 == tbl:deletes ==> Taxpayer3

    Event1 == peg:hasTimeAfter ==> EventTime1After
    Event1 == peg:hasTimeBefore ==> EventTime1Before
    Event1 == tbl:isEventType ==> Event1Type

    Event2 == peg:hasTime ==> Event2Time
    Event2 == tbl:isEventType ==> Event2Type

    %%Event3 == peg:hasTime ==> Event3Time
    %%Event3 == tbl:isEventType ==> Event3Type

    %%Event4 == peg:hasTimeAfter ==> Event4Time
    %%Event4 == tbl:isEventType ==> Event4Type
```

#### Exemple
![Folio 1090](./img/folio_champigny_FRAD094_3P_000108_01_0004.PNG "Archives Départementales du Val-de-Marne, 3P 108")