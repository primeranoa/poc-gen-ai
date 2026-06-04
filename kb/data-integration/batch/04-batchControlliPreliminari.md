# 04 — batchControlliPreliminari.xml

**Job Name:** `CONTROLLI PRELIMINARI`  
**Tipo:** SQL  
**Transazionale:** Si

## Scopo

Valida i dati importati nelle tabelle TMP_*, scartando record duplicati o con dati mancanti/inconsistenti.

## Controlli per flusso

| # | Tabella TMP | Chiave Controllo | Controlli |
|---|-------------|------------------|----------|
| 0 | TMP_ANAGRTIT | CODICE_TITOLO | Duplicati |
| 1 | TMP_PPEESG_INSTR_ATTRIBUTES | INSTRUMENT_CODE + PILLAR_KEY | Duplicati, score mancante |
| 2 | TMP_CATALOGOTM | CODICEBANCA + MODSOMM + CODICERISCHIO + TIPOCONTROLLO + DOMINIO | Duplicati, valori TM incompleti |
| 3 | TMP_SETUPTM | MODSOMM + CODICEBANCA + TIPOCONTROLLO + ESITO + PRODUCT_TYPE | Duplicati |
| 4 | TMP_FATTISPECIETM | CODICEBANCA + RAGGRUPPAMENTO + TIPOCONTROLLO + DOMINIO | Duplicati, controllo TM non valido |
| 5 | TMP_COSTI_STD_PRODOTTO | CODICEINTERNO + CODICECOSTO + SCAGLIONEDA + SCAGLIONEA | Duplicati |
| 6 | TMP_COSTI_STD_FATTISPECIE | CODICEBANCA + CODICERAGGRUPPAMENTO + CODICECOSTO | Duplicati |
| 7 | TMP_PAAMAPPATURA | CODICETITOLO + CODICE | Duplicati |
| 8 | TMP_PAAMAPPATURAVALUTARIA | CODICETITOLO + CODICE | Duplicati |
| 9 | TMP_PAAMAPPATURAGEOGRAFICA | CODICETITOLO + CODICEITEM | Duplicati |
| 10 | TMP_PAAMAPPATURASETTORIALE | CODICETITOLO + CODICEITEM | Duplicati |
| 11 | TMP_PAASCENAINDICI | ID_SCENARIO + CODICE_INDICE | Duplicati |
| 12 | TMP_ECCEZIONISWITCH | CODICE_SICAV + FAMIGLIA_IN + FAMIGLIA_OUT | Duplicati |
| 13 | TMP_CATALOGOCOMMERCIALE | CODICEBANCA + C_SEGMENTO + CODICEINTERNO | Duplicati |
| 14 | TMP_PPEPRAPROXY | CODICE_TITOLO | Duplicati |
| 15 | TMP_PPESTRUMCOEFF | C_INSTRUMENT + C_CONTROLLO | Duplicati |

## Logica comune

Per ogni controllo:
1. `INSERT INTO SCARTI_TMP_*` dei record problematici con MOTIVO_SCARTO
2. `DELETE FROM TMP_*` dei record scartati
