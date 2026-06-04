# 08 — batchStoricizzazioneConsulenza.xml

**Job Name:** `STORICIZZAZIONE CONSULENZA`  
**Tipo:** SQL  
**Transazionale:** Si

## Scopo

Crea snapshot storici dei parametri di consulenza (score, ESG). Eseguito sia per AA=1 che per AA=2.

## Entita storicizzate

| # | Tabella origine | Tabella BKP | Chiave |
|---|-----------------|-------------|--------|
| 0 | PPESCORE | PPESCORE_BKP | ISIN + CODE_BANCA + SERVIZIO + AMBITO_APPLICATIVO |
| 1 | PPEESG_INSTR_ATTRIBUTES | PPEESG_INSTR_ATTRIBUTES_BKP | INSTRUMENT_CODE + PILLAR_KEY |
| 2 | PPEESG_INSTR_ATTRIBUTES_MAN | PPEESG_INSTR_ATTR_MAN_BKP | INSTRUMENT_CODE + PILLAR_KEY |
| 3 | PPEESG_THRESHOLD | PPEESG_THRESHOLD_BKP | BANKING_GROUP + SERVICE_MODEL + CODE_ESG_THRESHOLD |
| 4 | PPEESG_PILLAR | PPEESG_PILLAR_BKP | BANKING_GROUP + SERVICE_MODEL + CODE_ESG_PILLAR |
| 5 | PPEESG_CHECK | PPEESG_CHECK_BKP | BANKING_GROUP + SERVICE_MODEL + CODE_CHECK |

## Pattern
3 step: chiudi modificati + inserisci nuovi + chiudi rimossi.
Campi temporali: START_DATE / END_DATE.
