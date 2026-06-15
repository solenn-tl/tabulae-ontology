# TABULAE Ontology : Temporal Attribute-Based Understanding of LAnd plots Evolution

This repository contains the documentation of the TABULAE ontology : <i>**T**emporal **A**ttribute-**B**ased **U**nderstanding of **LA**nd plots **E**volution</i>.
This ontology has been developped following the SAMOD methodology to represent land plots and their evolution using information from the documents of the (historical) land registry.
The TABULAE ontology has been developped as an extension of the PeGaZus ontology.

## Structure of the repository
```
├── data                   
│   ├── skos                        
│       ├── ttl            <- SKOS Concept Scheme as ttl
│
├── docs                   <- Widoco documentation
│
├── ontology 
│   ├── ontology-land-registry.ttl   <- Turtle implementation
│   ├── eng-documentation            <- Ontology documentation (english)
│       ├── geographical_entities
│       ├── taxpayers
│       ├── temporal_evolution
│       ├── land_registry_documents_use
│       ├── sources
│   ├── fr-documentation             <- Ontology documentation (french)
│       ├── entites_geographiques
│       ├── contribuables
│       ├── evolution_temporelle
│       ├── fonctionnement_cadastre
│       ├── sources
│
├── CITATION.cff
├── LICENCE.md
└── README.md
```

### `ontology` folder
*The documentation of the repo is currently upgraded with new schemas, examples. The french translation is also in preparation. It should be uploaded between june and july 2026.*

The TABULAE ontology implementation in RDF is available in `ontology-land-registry.ttl`. The detailed documentaation is provided in english and in french in the [ontology folder](ontology/eng-documentation). It is is divided into as many parts as there are modelets:
* [`landmarks`](ontology/documentation/eng-documentation/landmarks);
* [`land_registry_documents_use`](ontology/documentation/eng-documentation/land_registry_documents_use) ;
* [`sources`](ontology/documentation/eng-documentation/sources) ;
* [`taxpayers`](ontology/documentation/eng-documentation/taxpayers) ;
* [`temporal_evolution`](ontology/documentation/eng-documentation/temporal_evolution).

Each modelet documentation has 3 to 5 files:
* `{modelet_name}_scenario.md`: the natural-language argument describing the sub-problem to be addressed ;
* `{modelet_name}_glossary.md`: glossary which defines the main terms involved ;
* `{modelet_name}_competency_questions.md`: set of informal competence questions (in natural language) which represent the questions to be answered by the knowledge base ;
* `{modelet_name}_sparql_queries.md`: it translates informal competence questions into SPARQL queries ;
* `{modelet_name}_schema.md`: it proposes illustrated examples of the use of the TABULAE ontology, including association with the PeGazUs ontology.
 
### `docs` folder
This folder contains the official documentation of the ontology generated with Widoco. It also contains the OOPS! report associated.

## Used vocabularies
Following the recommandations of the W3C, this ontology reused concepts and properties of several pre-existant ontologies. It is also and extension of the PeGazUs ontology.
* PeGazUs
* Prov-O
* RiC-O
* Time

## Acknowledgements
This work was supported by the IGN and the AID.

## See also
* Detail description of the Tabulae ontology as well as the kg population algorithm for the land registry.
```
@phdthesis{tual:tel-05603252,
  TITLE = {{Reconstitution automatique de la généalogie des parcelles et des bâtiments à partir de sources historiques}},
  AUTHOR = {Tual, Solenn},
  URL = {https://theses.hal.science/tel-05603252},
  NUMBER = {2025UEFL2118},
  SCHOOL = {{Universit{\'e} Gustave Eiffel}},
  YEAR = {2025},
  MONTH = Dec,
  TYPE = {Theses},
  DOI = {10.70675/bbb45d62z6cedz4e17z98c8zb2a18b4f7aa9}
}
```
* First description of the association between PeGazUs and Tabulae. Description of the KG population algorithm.
```
@inproceedings{bernard:hal-04721538,
  TITLE = {{PeGazUs: A knowledge graph based approach to build urban perpetual gazetteers}},
  AUTHOR = {Bernard, Charly and Tual, Solenn and Abadie, Nathalie and Dum{\'e}nieu, Bertrand and Perret, Julien and Chazalon, Joseph},
  URL = {https://hal.science/hal-04721538},
  BOOKTITLE = {{International Conference on Knowledge Engineering and Knowledge Management (EKAW 2024)}},
  ADDRESS = {Amsterdam, Netherlands},
  PUBLISHER = {{Springer Nature Switzerland}},
  SERIES = {Lecture Notes in Computer Science},
  VOLUME = {15370},
  PAGES = {364-381},
  YEAR = {2024},
  MONTH = Nov,
  DOI = {10.1007/978-3-031-77792-9\_22},
}
```