# Sources 
This page includes additionnal documentation of the ```Sources``` modelet. it includes examples.

## Representation of the source documents and their derived content
### Example of <i>états de sections</i> (Initial register)
```mermaid
graph 
    %% 1. Nodes
    LRConceptNode("Cadastre (corpus)<br><small>a rico:RecordSet</small>")
    LRInstantiationNode("Cadastre (corpus) édition départementale<br><small>a rico:Instantiation</small>")

    RegisterConceptNode("Registre d'état de section de Marolles<br><small>a rico:Record</small>")
    PhysicalRegisterNode("Registre d'état de sections (physique), édition départementale<br><small>a rico:Instanciation</small>")
    ArchLocationLit["Archives départementales du Val-de-Marne"^^xsd:string]
    PubDate["1810"^^xsd:date]
    ArchivalReferenceLit["3P 387"^^xsd:string]
    DigitisedRegisterNode("Registre numérisé<br><small>a rico:Instanciation</small>")
    DigArchivalReferenceLit["FRAD094-3P-000387-01"^^xsd:string]

    ImageNode("Page de registre numérisée<br><small>a rico:Instanciation</small>")
    RefImageNode["FRAD094-3P-000387-0001"^^xsd:string]
    AnnotationClassInstBN((" "))
    tblAnnotationClass((tbl:AnnotationClass))
    SKOSPageClass(("anclass:ETSTab<br><small>a "))
    TreatedImageNode("Page de registre transcrite"<br><small>a rico:Instantiation</small>)
    TreatedImageNodeUUID["Identifiant UUID"^^xsd:literal]

    ClassificationActivity["000003<br><small>a prov:Activity</small>"]
    SoftwareAgentYolo["Modèle de classification<br><small>a prov:SoftwareAgent"]
    TranscriptionActivity01["000001<br><small>a prov:Activity</small>"]
    SoftwareAgentDAN["Modèle d'extraction d'informations<br><small>a prov:SoftwareAgent"]
    %%NERActivity["000002<br><small>a prov:Activity</small>"]
    %%SoftwareAgentCamembert["NER<br><small>a prov:SoftwareAgent"]

    RowNode("Ligne de registre<br><small> a rico:Instanciation</small>")
    LiteralFullRow["Les uselles de Marolles 60 Berthier Alexandre Prince de Neufchâtel Terre"^^xsd:string]
    IIIFImageUrlLiteral["https://archives.valdemarne.fr/_recherche-images/show/59414/image/38776/4/info.json"^^xsd:string]
    RowInteger[18^^xsd:integer]
    CoordsFullRow[1160,1103,1529,1421^^xsd:string]
    RowNodeClassBN((" "))
    RowNodeClass
    RowNodeClassValue((anclass:TableRow))
    RowIdentifier["Identifiant UUID"^^xsd:string]

    NamedEntityBN((" "))
    tblNamedEntity(("tbl:NamedEntity"))
    LiteralText["Berthier Alexandre Prince de Neufchâtel"^^xsd:string]
    LiteralStartChar["26"^^xsd:integer]
    LiteralStopChar["64"^^xsd:integer]
    SKOSEntityType(("anclass:Taxpayer"))

    %% 2. Edges
    LRConceptNode == rico:includesOrIncluded ==> RegisterConceptNode
    LRConceptNode == rico:hasInstantiation ==> LRInstantiationNode

    LRInstantiationNode == rico:physicalLocation ==> ArchLocationLit 
    RegisterConceptNode == rico:hasInstantiation ==> PhysicalRegisterNode
    LRInstantiationNode == rico:hasOrHadComponent ==> PhysicalRegisterNode
    PhysicalRegisterNode == rico:publicationDate ==> PubDate
    PhysicalRegisterNode == dcterms:identifer ==> ArchivalReferenceLit
    PhysicalRegisterNode == rico:hasDerivedInstantiation ==> DigitisedRegisterNode
    DigitisedRegisterNode == rico:hasOrHadComponent ==> ImageNode
    DigitisedRegisterNode == dcterms:identifer ==> DigArchivalReferenceLit

    ImageNode == "rico:hasOrHadDerivedInstantiation" ==> TreatedImageNode 
    TreatedImageNode == rico:hasOrHadComponent ==> RowNode
    TreatedImageNode == dcterms:identifier ==> TreatedImageNodeUUID
    ImageNode  == dcterms:identifer ==> RefImageNode
    ImageNode  == tbl:IIIFImageUrl ==> IIIFImageUrlLiteral
    ImageNode  == tbl:hasClass ==> AnnotationClassInstBN
    AnnotationClassInstBN == prov:wasGeneratedBy ==> ClassificationActivity
    ClassificationActivity == prov:wasAssociatedWith ==> SoftwareAgentYolo
    TranscriptionActivity01 == prov:used ==> ImageNode
    TranscriptionActivity01 == prov:wasAssociatedWith ==> SoftwareAgentDAN
    TreatedImageNode == prov:wasGeneratedBy ==> TranscriptionActivity01
    AnnotationClassInstBN == rdf:type ==> tblAnnotationClass
    AnnotationClassInstBN == tbl:hasClassValue ==> SKOSPageClass
    
    RowNode == tbl:transcription ==> LiteralFullRow
    RowNode == tbl:xywhCoordinates ==> CoordsFullRow
    RowNode == tbl:lineOrderInArea ==> RowInteger
    RowNode == tbl:hasNamedEntity ==> NamedEntityBN
    RowNode == tbl:hasClass ==> RowNodeClassBN
    RowNode == dcterms:identifier ==> RowIdentifier
    RowNodeClassBN == tbl:hasClassValue ==> RowNodeClassValue
    
    NamedEntityBN == rdf:type ==> tblNamedEntity
    NamedEntityBN == tbl:spanValue ==> LiteralText
    NamedEntityBN == tbl:indexOfFirstCharacter ==> LiteralStartChar
    NamedEntityBN == tbl:indexOfLastCharacter ==> LiteralStopChar
    NamedEntityBN == tbl:isNamedEntityType ==> SKOSEntityType
    %%NamedEntityBN == prov:wasGeneratedBy ==> NERActivity
    %%NERActivity == prov:used ==> RowNode
    %%NERActivity == prov:wasAssociatedWith ==> SoftwareAgentCamembert

    %% 3. Apply WebVOWL Style
    classDef vowlClass fill:#aaccff,stroke:#3366cc,stroke-width:2px,color:#000,font-weight:bold;
    classDef vowlLiteral fill:#ffffcc,stroke:#ffcc00,stroke-width:2px,color:#000;
    classDef vowlInstance fill:#ece0f8,stroke:#d397d3,stroke-width:2px,color:#000;
    classDef vowlValue fill:#ffffcc,stroke:#ffcc00,stroke-width:1px,color:#000,font-family:monospace;
    %% Skos
    classDef vowlClassInstance fill:#CB8DD6,stroke:#5F2569,stroke-width:2px,color:#000,font-weight:bold;
    %% Blank node
    classDef blankNode fill:#ffffff,stroke:#888888,stroke-width:2px,stroke-dasharray: 4;

    class LRConceptNode,LRInstantiationNode,RegisterConceptNode,PhysicalRegisterNode,DigitisedRegisterNode,ImageNode,TreatedImageNode,RowNode vowlInstance;

    class ArchLocationLit,PubDate,ArchivalReferenceLit,DigArchivalReferenceLit,RefImageNode,LiteralFullRow,IIIFImageUrlLiteral,RowInteger,CoordsFullRow,TreatedImageNodeUUID,LiteralText,LiteralStartChar,LiteralStopChar,RowIdentifier vowlLiteral;

    class AnnotationClassInstBN,NamedEntityBN,RowNodeClassBN blankNode;

    class tblAnnotationClass,tblNamedEntity vowlClass;

    class SKOSPageClass,SKOSEntityType,RowNodeClass vowlClassInstance;
```
#### Notes
* ```prov:Activity``` has additionnal properties (start date, end date).
* ```prov:Agent``` and ```prov:SoftwareAgent``` also have additionnal properties.

### Example of <i>matrice</i> (Initial register)
*To be added*

## Taxonomy
### Type of sources
* URI : ```https://w3id.org/tabulae#LandRegistrySourceList```
```mermaid
graph LR
    %% Déclaration de TOUS les concepts (y compris isolés)
    ArticleDeClassement["Article de classement"]
    ArticleDeMutation["Article de mutation"]
    CompteFoncier["Compte foncier"]
    EtatsDeSections_Ap_1822["Etats de sections postérieurs à 1822"]
    EtatsDeSections_Av_1822_Bati["Etats de sections antérieurs à 1822 (propriétés bâties)"]
    EtatsDeSections_Av_1822_NonBati["Etats de sections antérieurs à 1822 (propriétés non bâties)"]
    EtatsDeSections_Scp_Seine_1835["Etats de sections spécifiques à la rénovation du cadastre de la Seine (1835-1845)"]
    FicheInventaire["Inventaire des archives"]
    FolioBati["Folio (Bâti)"]
    FolioNonBati["Folio (Non Bâti)"]
    LigneEtatDeSection["Ligne de tableau d'états de sections"]
    MatriceCadastrale1807_1822_Bati_NonBati["Matrice de rôles des propriétés bâties et non bâties (1807-1822)"]
    MatriceCadastrale1822_1914_NonBati["Matrice des propriétés non bâties (1822-1914)"]
    MatriceCadastrale1882_1911_Bati["Matrice des propriétés bâties (1882-1911)"]
    MatriceCadastrale1911_Renovation_Bati["Matrice des propriétés bâties (1911-rénovation)"]
    MatriceCadastrale1914_Renovation_NonBati["Matrice des propriétés non bâties (1914-rénovation)"]
    Ouvrage["Ouvrage"]
    PlanGeoreference["Plan vectorisé"]
    PlanParcellaireIssuDAtlas["Plan parcellaire issu d'atlas"]
    PlanParcellaireMinute["Plan parcellaire : minute"]
    PlanVectorise["Plan géoréférencé"]
    TableauAssemblage["Tableau d'assemblage"]
    PageDeRegistre["Page de registre cadastral"]
    PlanParcellaireFinal["Plan parcellaire final"]
    Cadastre["Cadastre"]
    EtatsDeSections_Av_1822["Etats de sections antérieurs à 1822"]
    Folio["Folio"]
    PlanParcellaire["Plan parcellaire"]
    EtatsDeSections["Etats de sections"]
    RegistreCadastral["Registre cadastral"]
    Plan["Plan"]
    MatriceCadastrale["Matrice cadastrale"]
    ZoneDePage["Zone située dans une page de registre cadastral"]

    %% Déclaration des relations
    Cadastre -->|broader| Plan
    MatriceCadastrale -->|broader| MatriceCadastrale1882_1911_Bati
    Cadastre -->|broader| RegistreCadastral
    PlanParcellaire -->|broader| PlanParcellaireFinal
    EtatsDeSections_Av_1822 -->|broader| EtatsDeSections_Av_1822_Bati
    PlanParcellaireFinal -->|broader| PlanParcellaireIssuDAtlas
    ZoneDePage -->|broader| ArticleDeClassement
    ZoneDePage -->|broader| LigneEtatDeSection
    EtatsDeSections_Av_1822 -->|broader| EtatsDeSections_Av_1822_NonBati
    Plan -->|broader| PlanParcellaire
    EtatsDeSections -->|broader| EtatsDeSections_Av_1822
    RegistreCadastral -->|broader| MatriceCadastrale
    MatriceCadastrale -->|broader| MatriceCadastrale1911_Renovation_Bati
    RegistreCadastral -->|broader| PageDeRegistre
    PlanParcellaire -->|broader| PlanParcellaireMinute
    Plan -->|broader| PlanVectorise
    MatriceCadastrale -->|broader| MatriceCadastrale1822_1914_NonBati
    Folio -->|broader| FolioBati
    PageDeRegistre -->|broader| ZoneDePage
    RegistreCadastral -->|broader| EtatsDeSections
    Folio -->|broader| FolioNonBati
    CompteFoncier -->|broader| Folio
    ZoneDePage -->|broader| CompteFoncier
    EtatsDeSections -->|broader| EtatsDeSections_Scp_Seine_1835
    MatriceCadastrale -->|broader| MatriceCadastrale1807_1822_Bati_NonBati
    ZoneDePage -->|broader| Folio
    EtatsDeSections -->|broader| EtatsDeSections_Ap_1822
    MatriceCadastrale -->|broader| MatriceCadastrale1914_Renovation_NonBati
    Plan -->|broader| TableauAssemblage
    ZoneDePage -->|broader| ArticleDeMutation
    Plan -->|broader| PlanGeoreference
```

## References
* For provenance description :
```plaintext 
Melvin Hersent, Abadie Nathalie, Duménieu Bertrand, Perret Julien. Modèles et outils pour la publication de métadonnées d'archives géographiques et de leurs données dérivées. Humanistica 2023, Association francophone des humanités numériques, Jun 2023, Genève, Suisse. pp.hal-04110787. ⟨hal-04110787⟩
```