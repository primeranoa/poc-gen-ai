# 03 — batchImportazione.xml

**Job Name:** `FASE IMPORTAZIONE FLUSSI DI INPUT`  
**Tipo:** SQL + Import + Java (multithread)

## Scopo

Carica i file CSV/TXT nelle tabelle temporanee (TMP_*). I 3 flussi piu voluminosi (mappatura, anagrtit, catalogotm) vengono importati in parallelo via multithread Java.

## Task

| # | Condizione (enabled) | Tracciato XML | Tabella TMP | Note |
|---|---------------------|---------------|-------------|------|
| 0 | BATCH_ENABLE_TASK_MAPPATURAVALUTARIA | mappaturavalutaria.xml | TMP_PAAMAPPATURAVALUTARIA | |
| 1 | BATCH_ENABLE_TASK_SCENAINDICI | scenaindici.xml | TMP_PAASCENAINDICI | |
| 2 | BATCH_ENABLE_TASK_MAPPATURA | — (solo pulizia scarti) | — | Import nel task 5 |
| 3 | Sempre | — (solo pulizia scarti) | — | Import nel task 5 |
| 4 | Sempre | — (solo pulizia scarti) | — | Import nel task 5 |
| **5** | **Sempre** | **MULTITHREAD** | **TMP_PAAMAPPATURA + TMP_ANAGRTIT + TMP_CATALOGOTM** | **Parallelizzato** |
| 6 | Sempre | setuptm.xml | TMP_SETUPTM | |
| 7 | Sempre | fattispecietm.xml | TMP_FATTISPECIETM | |
| 8 | Sempre | costi_std_prodotto.xml | TMP_COSTI_STD_PRODOTTO | |
| 9 | Sempre | costi_std_fattispecie.xml | TMP_COSTI_STD_FATTISPECIE | |
| 10 | BATCH_ENABLE_TASK_SCENAINDICIGREZZE | scenaindicigrezze.xml | TMP_PAASCENAINDICIGREZZE | |
| 11 | Sempre | eccezioniswitch.xml | TMP_ECCEZIONISWITCH | |
| 12 | BATCH_ENABLE_TASK_MAPPATURAGEOGRAFICA | mappaturageografica.xml | TMP_PAAMAPPATURAGEOGRAFICA | |
| 13 | BATCH_ENABLE_TASK_MAPPATURASETTORIALE | mappaturasettoriale.xml | TMP_PAAMAPPATURASETTORIALE | |
| 14 | BATCH_ENABLE_TASK_IMPORT_CATALOGOCOMMERCIALE | catalogocommerciale.xml | TMP_CATALOGOCOMMERCIALE | |
| 15 | BATCH_ENABLE_TASK_IMPORT_PRAPROXY | praproxy.xml | TMP_PPEPRAPROXY | |
| 16 | BATCH_ENABLE_TASK_ESG | esg.xml | TMP_PPEESG_INSTR_ATTRIBUTES | |
| 17 | BATCH_ENABLE_TASK_ANASTRUMCOEFFICIENTI | anaStrumCoefficienti.xml | TMP_PPESTRUMCOEFF | |
| 18 | BATCH_ENABLE_TASK_IMPORT_CANALE_DISTRIBUZIONE | catalogocanaliprodotto.xml | TMP_CATCANALIPRODOTTO | |

## Task 5 — Importazione Multithread

**Classe Java:** `it.prometeia.batch.importa.model.ImportMultiThreadJob`

Importa in parallelo 3 flussi voluminosi:
1. `mappatura.xml` → TMP_PAAMAPPATURA
2. `anagrtit.xml` → TMP_ANAGRTIT
3. `catalogotm.xml` → TMP_CATALOGOTM

## Pattern per ogni task standard
1. `DELETE FROM SCARTI_TMP_*` — svuota tabella scarti
2. Import dal tracciato XML — carica CSV/TXT nella tabella TMP_*
