# Illustrated documentation of Taxpayers

This page proposes illustrated representation of the ```Taxpayer``` sub-module of the *PeGazUs* ontology.
Please refer to the ontology to get the full definitions of each property.

## Ontology
### Datatype properties
```mermaid
graph 
    %% 1. Nodes
    TaxpayerNode(("tbl:Taxpayer"))
    LabelLit["string"]
    NameLit["string"]
    LastNameLit["string"]
    FirstNamesLit["string"]
    BirthNameLit["string"]
    SpouseOrChildrenFirstNames["string"]
    OrganisationNameLit["string"]
    ActivityLit["string"]
    AddressLit["string"]
    FamilyStatusLit["string"]
    TitleLit["string"]

    %% 2. Connect the unique IDs
    
    TaxpayerNode == "tbl:taxpayerLabel" ==> LabelLit 
    TaxpayerNode == "tbl:taxpayerFullName" ==> NameLit 
    TaxpayerNode == "tbl:taxpayerLastName" ==> LastNameLit
    TaxpayerNode == "tbl:taxpayerFirstNames" ==> FirstNamesLit
    TaxpayerNode == "tbl:taxpayerBirthName" ==> BirthNameLit
    TaxpayerNode == "tbl:taxpayerSpouseOrChildrenFirstNames" ==> SpouseOrChildrenFirstNames
    TaxpayerNode == "tbl:taxpayerOrganisationName" ==> OrganisationNameLit
    TaxpayerNode == "tbl:taxpayerActivity" ==> ActivityLit
    TaxpayerNode == "tbl:taxpayerAddress" ==> AddressLit
    TaxpayerNode == "tbl:taxpayerFamilyStatus" ==> FamilyStatusLit
    TaxpayerNode == "tbl:taxpayerTitle" ==> TitleLit

    %%LabelLit ~~~ NameLit ~~~ LastNameLit ~~~ FirstNamesLit ~~~ BirthNameLit ~~~ SpouseOrChildrenFirstNames ~~~ OrganisationNameLit ~~~ ActivityLit ~~~ AddressLit ~~~ FamilyStatusLit ~~~ TitleLit

    %% 3. Apply WebVOWL Style
    classDef vowlClass fill:#aaccff,stroke:#3366cc,stroke-width:2px,color:#000,font-weight:bold;
    classDef vowlLiteral fill:#ffffcc,stroke:#ffcc00,stroke-width:2px,color:#000;

    class TaxpayerNode vowlClass;
    class LabelLit,NameLit,LastNameLit,FirstNamesLit,ActivityLit,AddressLit,TitleLit,OrganisationNameLit,SpouseOrChildrenFirstNames,BirthNameLit,FamilyStatusLit vowlLiteral;
```
### Object properties
```mermaid
graph 
    %% 1. Nodes
    TaxpayerNode(("tbl:Taxpayer"))
    AddressThingNode(("owl:Thing"))

    %% 2. Connect the unique IDs
    TaxpayerNode == "tbl:taxpayerAddressEntity" ==> AddressThingNode

    %% 3. Apply WebVOWL Style
    classDef vowlClass fill:#aaccff,stroke:#3366cc,stroke-width:2px,color:#000,font-weight:bold;
    %% WebVOWL Style for owl:Thing
    classDef vowlThing fill:#f5f5f5,stroke:#999999,stroke-width:2px,stroke-dasharray: 4,color:#000,font-style:italic;
    
    class TaxpayerNode,AddressEnt vowlClass;
    class AddressThingNode vowlThing;
```
### Note
* ```tbl:taxpayerLabel``` is a super-property for ```tbl:taxpayerFullName``` (natural person) and ```tbl:taxpayerOrganisationName``` (legal person). It can be used when the kind of taxpayer is not known.
* ```tbl:taxpayerAddressEntity``` can be used when the value associated to ```tbl:taxpayerAddress``` as been linked to any geographical entity of a KG. For instance, it can be an ```addr:Landmark``` entity.
* Upcomming developpements will create object properties for actitivies, family status and titles.

## Examples
*Barbaroux quincailler à Paris*
```mermaid
graph 
    %% ----- Noeuds -----
    %% 1. Syntaxe : ID("Nom affiché <br> <i>[Type de la classe]</i>")
    TaxpayerInst("taxpayer:barbaroux<br><small>a tbl:Taxpayer</small>")
    
    %% Littéraux (Valeurs concrètes de Datatype Properties)
    FullNameLit["'Barbaroux'^^xsd:string"]
    LastNameLit["'Barbaroux'^^xsd:string"]
    ActivityLit["'quincailler'^^xsd:string"]
    AddressLit["'Paris'^^xsd:string"]

    %% ------ Relations -------
    %% Object Property (Lien entre individus) : Ligne pleine
    %% TaxpayerInst -- "tbl:hasAddress" --> AddressInst
    
    %% Datatype Properties
    TaxpayerInst -- "tbl:taxpayerFullName" --> FullNameLit
    TaxpayerInst -- "tbl:taxpayerLastName" --> LastNameLit
    TaxpayerInst -- "tbl:taxpayerActivity" --> ActivityLit
    TaxpayerInst -- "tbl:taxpayerAddress" --> AddressLit

    %% ------- STYLES ------
    %% Violet VOWL pour les instances
    classDef vowlInstance fill:#ece0f8,stroke:#d397d3,stroke-width:2px,color:#000;
    %% Jaune VOWL pour les valeurs litérales
    classDef vowlValue fill:#ffffcc,stroke:#ffcc00,stroke-width:1px,color:#000,font-family:monospace;

    %% Application des styles aux données
    class TaxpayerInst,InstanceNode vowlInstance;
    class FullNameLit,LastNameLit,AddressLit,ActivityLit,LiteralVal vowlValue;
    class Src1,Tgt1,Src2,Tgt2 invisible;

    %% Couleur violette pour les flèches d'Object Properties (Liens entre instances)
    %% Index 0 (hasAddress) et Index 2 (Légende Object Property)
    %% linkStyle 0,2 stroke:#b573b5,stroke-width:2px;
```
*Pravel Louis Ve née Gerbuisson*
```mermaid
graph 
    %% ----- Noeuds -----
    %% 1. Syntaxe : ID("Nom affiché <br> <i>[Type de la classe]</i>")
    TaxpayerInst2("taxpayer:pravel_louis_vve<br><small>a tbl:Taxpayer</small>")
    
    %% Littéraux (Valeurs concrètes de Datatype Properties)
    FullNameLit["'Pravel Louis Ve née Gerbuisson'^^xsd:string"]
    LastNameLit["'Pravel'^^xsd:string"]
    FirstNamesLit["'Louis'^^xsd:string"]
    FamilyStatusLit["'Ve'^^xsd:string"]
    BirthNameLit["'Gerbuisson'^^xsd:string"]
    
    %% Datatype Properties
    TaxpayerInst2 -- "tbl:taxpayerFullName" --> FullNameLit
    TaxpayerInst2 -- "tbl:taxpayerLastName" --> LastNameLit
    TaxpayerInst2 -- "tbl:taxpayerFirstNames" --> FirstNamesLit
    TaxpayerInst2 -- "tbl:taxpayerFamilyStatus" --> FamilyStatusLit
    TaxpayerInst2 -- "tbl:taxpayerBirthName" --> BirthNameLit

    %% ------- STYLES ------
    %% Violet VOWL pour les instances
    classDef vowlInstance fill:#ece0f8,stroke:#d397d3,stroke-width:2px,color:#000;
    %% Jaune VOWL pour les valeurs litérales
    classDef vowlValue fill:#ffffcc,stroke:#ffcc00,stroke-width:1px,color:#000,font-family:monospace;

    %% Application des styles aux données
    class TaxpayerInst2,InstanceNode vowlInstance;
    class FullNameLit,LastNameLit,FirstNamesLit,FamilyStatusLit,BirthNameLit,LiteralVal vowlValue;
    class Src1,Tgt1,Src2,Tgt2 invisible;

    %% Couleur violette pour les flèches d'Object Properties (Liens entre instances)
    %% Index 0 (hasAddress) et Index 2 (Légende Object Property)
    %% linkStyle 0,2 stroke:#b573b5,stroke-width:2px;
```