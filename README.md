# Forensic Data Architecture: Mapping Opaque Asset Flow

## Project Overview
This repository houses structural data schemas designed to model illicit asset movement, provenance fragmentation, and ultimate beneficial ownership (UBO) networks. The objective is to translate qualitative provenance anomalies into machine-readable network graphs for regulatory compliance, KYC, and anti-money laundering (AML) screening.

## Case Study 1: The Ars Juris Gift & Nazi-Era Provenance
Based on the *Ars Juris* Research Memorandum, this data schema normalizes disparate archival transaction logs into an entity-resolution model. It tracks the physical migration of Pierre Bonnard’s *Reclining Woman on Bed* (1897) through conflicting Nazi confiscation registries (ERR Database) and post-war custodial gaps.

### Entity Relationship Model (Relational Schema)


| Table Name | Primary Key | Attributes / Metadata Captured | Foreign Keys |
| :--- | :--- | :--- | :--- |
| **Asset_Registry** | `Asset_ID` | Title, Artist, Creation_Year, Catalogue_Raisonné_Status | `Provenance_ID` |
| **Entity_Registry**| `Entity_ID` | Entity_Name, Entity_Type (Individual/State/Shell) | `Location_ID` |
| **Custody_Event**  | `Event_ID` | Event_Type (Looting/Sale/Gift), Date, Document_Source | `Asset_ID`, `Source_Entity_ID`, `Target_Entity_ID` |
| **Legal_Risk_Log** | `Risk_ID` | Statutory_Framework (HEAR Act/CPIA), Claim_Window_Status | `Asset_ID` |


## System Visualization Flowchart

```mermaid
graph LR
    A[Madame Kapferer <br><i>Original Owner</i>] --> B(Château de Brissac <br><i>Intake Facility</i>)
    B -->|Flag: ERR Entry| C(Jeu de Paume <br><i>Nazi Custody</i>)
    C -->|Null Pointer Resolution Risk| D{PROVENANCE GAP <br>1953 - 2026}
    D -->|Title Liability Under HEAR Act| E[Ars Juris Estate <br><i>Donor</i>]

    style A fill:#edf2f7,stroke:#4a5568,stroke-width:2px;
    style B fill:#edf2f7,stroke:#4a5568,stroke-width:2px;
    style C fill:#edf2f7,stroke:#4a5568,stroke-width:2px;
    style D fill:#fee8e8,stroke:#e53e3e,stroke-width:2px,color:#9b2c2c;
    style E fill:#edf2f7,stroke:#4a5568,stroke-width:2px;
```
## Algorithmic Logic & Red Flag Diagnostics
The data model translates historical text documents into directed edges to calculate structural risk metrics:

