## Légende des schémas
### Diagrammes de classe
* Chaque boîte est une classe OWL ; les propriétés littérales (datatype properties) sont listées dans la boîte, avec leur type XSD.
* Les flèches pleines (```-->```) sont des propriétés objet, orientées du domaine vers le range.
* Les boîtes ```«SKOSConcept»``` sont des individus issus des schémas de concepts SKOS ; la flèche pointillée ```rdf:type``` indique leur classe.
* Un range défini comme union de classes (```owl:unionOf```) est représenté par une flèche vers chaque classe membre, portant le même libellé de propriété. Par exemple, ```tbl:hasPlotAddress``` a trois flèches, vers ```peg:Address```, ```peg:LandmarkRelation``` et ```peg:Landmark```.
* Les multiplicités (```1```, ```0..1```) traduisent les restrictions de cardinalité qualifiées de PeGazUs. Une flèche sans multiplicité n'a pas de restriction.
* Les classes ```peg:*``` sont définies dans [PeGazUs](pegazus.ttl), les classes ```tbl:*``` et les concepts ```tblltype:*```, ```tblatype:*``` dans TABULAE.
* Couleurs par ontologie  :

  <!-- sync:styles-legende:start -->
  | Ontologie | Style Mermaid | Rendu |
  |---|---|---|
  | TABULAE (```tbl:```) | ```tbl``` | vert vif, bordure épaisse |
  | TABULAE, concepts SKOS (```tblltype:```, ```tblatype:```, …) | ```tblConcept``` | vert clair, bordure pointillée |
  | PeGazUs (```peg:```) | ```peg``` | bleu clair |
  | SKOS (```skos:```) | ```skos``` | orange clair |
  | RiC-O (```rico:```) | ```rico``` | mauve clair |
  | Unions (```owl:unionOf```) | ```owlUnion``` | gris, bordure pointillée |
  <!-- sync:styles-legende:end -->