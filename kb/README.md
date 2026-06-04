# POC_GEN_AI

## Overview

- **Database engine:** PostgreSQL (AWS RDS) — stessa infrastruttura PROMPFT
- **Schema:** PPE/PFP (prefisso tabelle)
- **Ambienti:** AA=1 (principale), AA=2 (allineamento giornaliero)
- **Segmenti serviti:** Consulenza base, Consulenza privata
- **Stack applicativo:** Java 8, Spring, Hibernate, Jersey JAX-RS, JSF/PrimeFaces
- **Deployment:** AWS (S3 sync per file I/O), Docker-based batch
- **Infrastruttura:** S3 bucket per scambio file, Redis/DynamoDB per cache
- **POC specifics:** Script Python per trasformazione flussi da altri clienti (es. BMED)

## Struttura Documentazione

| Sezione | Descrizione | Stato |
|---------|-------------|-------|
| [Data Integration](data-integration/) | Flussi batch import/export (20 batch) | ✅ Completato |
| [Procedure](../procedure/) | Script Python di conversione | ✅ Completato |
| [Architettura](architettura/) | Stack tecnico, pattern architetturale | ⬜ Da fare |
| [Funzionale](funzionale/) | Documentazione moduli applicativi | ⬜ Da fare |
| [Database](database/) | Schema DB organizzato per funzionalità | ⬜ Da fare |

## Caratteristiche specifiche (ereditate da PROMPFT)

- **Importazione multithread:** mappatura, anagrtit e catalogotm importati in parallelo
- **Flussi condizionali (enabled):** molti task attivati/disattivati via variabili d'ambiente
- **Doppio ambito applicativo:** AA=1 (principale) e AA=2 (allineamento giornaliero)
- **AWS integration:** S3 sync per input/output file, deploy su cloud
- **Cache multipla:** SqlDb, Redis, DynamoDB
- **Esportazione multipla:** ADVEngine, ADVEngineSP (Service Pack), PPE, CAT (Catalogo)
- **ESG** con attributi strumento
- **Mappatura estesa:** valutaria, geografica, settoriale
- **Scenari indici** (normali + grezzi)
- **Eccezioni switch** tra prodotti

## Procedure AI-Assisted

| Script | Descrizione |
|--------|-------------|
| `procedure/converti_anatit_bmed_to_prompft.py` | Converte ANATIT BMED (165 col) → PFPANATIT PROMPFT (177 col) |
