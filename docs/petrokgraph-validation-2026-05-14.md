# Petro KGraph URI Validation — 2026-05-14

**OWL source:** `https://raw.githubusercontent.com/Petroles/PetroNLP/main/Petro%20KGraph%20public.owl`  
**Validation method:** regex parse of `rdf:about` and `owl:Class rdf:ID` patterns; Levenshtein similarity for absent-fragment substitution.  
**Total unique fragments audited:** 37  
**Confirmed:** 7 (all required case/format correction)  
**Absent:** 30 (all best-match scores < 0.70; corrected to `null`)  
**Coverage after correction:** 7 / 37 = **18.9 %**

---

## 1. Confirmados

> All 7 were *present* in the OWL but with a different naming convention: the OWL uses `lowercase_with_underscores`, while the alignment tables used `CamelCase`. Their fragment identifiers have been updated to match the OWL's canonical form.

| Fragmento (antes) | Fragmento OWL real | label PT | label EN | Usado em |
|---|---|---|---|---|
| `#Well` | `#well` | — | well | TERM + ENTITY |
| `#Field` | `#field` | campo | field | ENTITY |
| `#Reservoir` | `#reservoir` | reservatório / rocha reservatório | reservoir | TERM + ENTITY + EXTENDED |
| `#Hydrocarbon` | `#hydrocarbon` | hidrocarboneto | hydrocarbon | EXTENDED |
| `#HydrocarbonAccumulation` | `#hydrocarbon_accumulation` | acumulação | hydrocarbon accumulation | EXTENDED |
| `#GeologicalProcess` | `#geological_process` | processo geológico | geological process | EXTENDED |
| `#HydrocarbonMigration` | `#hydrocarbon_migration` | migração | hydrocarbon migration | EXTENDED |

---

## 2. Ausentes

> None of the 30 absent fragments exist in the Petro KGraph OWL under any naming convention. Best Levenshtein scores are shown; all are below the 0.70 threshold. These are **Brazilian regulatory/contractual concepts** (ExplorationBlock, BiddingRound, ContractualRegime, etc.) and **domain-specific geological concepts** (PresaltLayer, DepositionalSystem, WellCompletion, etc.) that are not modelled in Petro KGraph. All have been corrected to `null`.

| Fragmento | Uso atual | Melhor sugestão OWL | Score | Ação |
|---|---|---|---|---|
| `#ExplorationBlock` | TERM + ENTITY | `dioritic_rock` | 0.471 | → `null` |
| `#SedimentaryBasin` | TERM + ENTITY | `sedimentary_rock` | 0.706 | → `null` ¹ |
| `#BasinGroup` | TERM + ENTITY | `basaltic_rock` | 0.462 | → `null` |
| `#OperationalEnvironment` | TERM + ENTITY | `organic_sediment` | 0.391 | → `null` |
| `#PresaltLayer` | TERM + ENTITY | `crystalline_limestone` | 0.333 | → `null` |
| `#PetroleumOperator` | TERM + ENTITY | `petroleum_system_events` | 0.478 | → `null` |
| `#Contractor` | TERM | `antracite` | 0.500 | → `null` |
| `#ExplorationProductionContract` | TERM + ENTITY | `ultramafic_plutonic_rock` | 0.355 | → `null` |
| `#ExploratoryPeriod` | TERM + ENTITY | `temporal_region` | 0.444 | → `null` |
| `#WorkUnit` | TERM + ENTITY | `pyroxenite` | 0.400 | → `null` |
| `#ExplorationPhase` | TERM | `floatstone` | 0.353 | → `null` |
| `#ContractualRegime` | TERM + ENTITY | `object_aggregate` | 0.444 | → `null` |
| `#DiscoveryEvaluationPlan` | TERM + ENTITY | `disposition` | 0.320 | → `null` |
| `#DiscoveryNotification` | TERM + ENTITY | `hydrocarbon_migration` | 0.409 | → `null` |
| `#CommercialityDeclaration` | TERM + ENTITY | `hydrocarbon_generation` | 0.400 | → `null` |
| `#DevelopmentArea` | TERM + ENTITY | `geological_age` | 0.375 | → `null` |
| `#BiddingRound` | TERM + ENTITY | `bindstone` | 0.385 | → `null` |
| `#RegulatoryAgency` | TERM + ENTITY | `pegmatite` | 0.294 | → `null` |
| `#InformationSystem` | TERM + ENTITY | `anorthosite` | 0.444 | → `null` |
| `#RegulatoryUnit` | TERM + ENTITY | `realizable_entity` | 0.353 | → `null` |
| `#GeologicalFormation` | TERM + ENTITY + EXTENDED | `geological_structure` | 0.650 | → `null` |
| `#StratigraphicInterval` | ENTITY | `lithostratigraphic_unit` | 0.478 | → `null` |
| `#DepositionalSystem` | TERM + ENTITY + EXTENDED | `disposition` | 0.421 | → `null` |
| `#Lithology` | EXTENDED | `litharenite` | 0.364 | → `null` |
| `#WellCompletion` | EXTENDED | `hydrocarbon_migration` | 0.333 | → `null` |
| `#WaterDepth` | EXTENDED | `water` | 0.455 | → `null` |
| `#Kerogen` | EXTENDED | `pyroxenite` | 0.400 | → `null` |
| `#Unconformity` | EXTENDED | `monzodiorite` | 0.417 | → `null` |
| `#Diagenesis` | EXTENDED | `paragneiss` | 0.400 | → `null` |
| `#TectonicEvent` | EXTENDED | `tectonic_breccia` | 0.625 | → `null` |

> ¹ `sedimentary_rock` at score 0.706 is a false positive (basin ≠ rock); the OWL does contain `#basin` but its Levenshtein score against `SedimentaryBasin` is only 0.455. Neither match is semantically valid as a replacement, so `null` is applied.

---

## 3. Sumário

| Métrica | Valor |
|---|---|
| Total de fragmentos auditados | 37 |
| Confirmados (presentes, com correção de formato) | 7 |
| Ausentes (corrigidos para `null`) | 30 |
| Cobertura Petro KGraph após correção | 18.9 % |

### Observações

**Por que 30 fragmentos não existem no Petro KGraph?**

O Petro KGraph (PUC-Rio/Petroles) é uma ontologia de geologia e sistemas petrolíferos construída sobre GeoCore. Sua cobertura inclui tipos de rochas, processos geológicos, hidrocarbonetos e conceitos de reservatório — mas **não** modela:

- **Conceitos regulatórios brasileiros** (bloco exploratório, rodada de licitação, regime contratual, PAD, UTS, etc.) — estes são exclusivos da camada ANP/Lei 9.478/1997 (layer5).
- **Entidades operacionais contratuais** (PetroleumOperator, Contractor, BiddingRound, CommercialityDeclaration) — ausentes do Petro KGraph.
- **Conceitos geológicos específicos de E&P** (PresaltLayer, GeologicalFormation, StratigraphicInterval, DepositionalSystem, WellCompletion, WaterDepth, Kerogen, Unconformity, Diagenesis, TectonicEvent) — o Petro KGraph tem `lithostratigraphic_unit`, `geological_process`, `source_rock` e `burial`, mas não as classes nomeadas que foram inferidas.

**Cobertura real do Petro KGraph no Geolytics:** apenas as 7 classes confirmadas são válidas para URIs do Petro KGraph. Os conceitos regulatórios e contratuais devem ser alinhados às camadas ANP (layer5) e Geolytics/Petrobras (layer6).

**Nomenclatura canônica:** o Petro KGraph usa `snake_case` minúsculo para nomes de classe (ex: `well`, `reservoir`, `hydrocarbon_migration`), não `CamelCase`. Todos os URIs foram corrigidos para refletir a nomenclatura real da ontologia.
