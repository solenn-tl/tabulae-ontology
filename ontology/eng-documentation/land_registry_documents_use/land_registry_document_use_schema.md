# Schemas related to the "Land registry document use" modelet

## Taxonomy
### Special values in tables, mostly in "Tiré de" et "Porté à" columns
* ```https://w3id.org/tabulae#SpecialCellValuesList```
```mermaid
graph LR
    %% Déclaration de TOUS les concepts (y compris isolés)
    AdditionConstructionSV["Addition à une construction"]
    AugmentationSV["Augmentation"]
    CelluleVide["Cellule vide"]
    ConstructionNouvelleSV["Construction nouvelle"]
    DemolitionSV["Démolition"]
    DiminutionSV["Diminution"]
    DoubleEmploiSV["Double emploi"]
    EvaluationSV["Evaluation"]
    IdemSV["Idem"]
    IdemPrecedentSV["Idem à la valeur de la cellule précédente"]
    IdemSuivantSV["Idem à la valeur de la cellule suivante"]
    InconnuSV["Valeur inconnue"]
    OmissionSV["Omission"]
    PartieSV["Partie"]
    ResteSV["Reste"]
    RuinesSV["En ruines"]
    ValeurBarreeSV["Valeur barrée"]
    VoiePubliqueSV["Passé à la voie publique"]

    %% Déclaration des relations
    IdemSV -->|broader| IdemPrecedentSV
    IdemSV -->|broader| IdemSuivantSV
```