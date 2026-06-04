
# POC_GEN_AI — Tracciati Input (Dettaglio Completo)

## Riepilogo File

| # | File CSV/TXT | Tabella TMP | Tabella Scarti | Chiave Primaria | Condizione |
|---|-------------|-------------|----------------|-----------------|------------|
| 1 | PFPANATIT.csv | TMP_ANAGRTIT | SCARTI_TMP_ANAGRTIT | CODICE_TITOLO | Sempre |
| 2 | TM_Actual.csv | TMP_CATALOGOTM | SCARTI_TMP_CATALOGOTM | CODICEBANCA+MODSOMM+CODICERISCHIO+TIPOCONTROLLO+DOMINIO | Sempre |
| 3 | TM_Appoggio.csv | TMP_SETUPTM | SCARTI_TMP_SETUPTM | MODSOMM+CODICEBANCA+TIPOCONTROLLO+ESITO+PRODUCT_TYPE | Sempre |
| 4 | TM_Fattispecie.csv | TMP_FATTISPECIETM | SCARTI_TMP_FATTISPECIETM | CODICEBANCA+RAGGRUPPAMENTO+TIPOCONTROLLO+DOMINIO | Sempre |
| 5 | costiStandardProdotto.csv | TMP_COSTI_STD_PRODOTTO | SCARTI_TMP_COSTI_STD_PRODOTTO | CODICEINTERNO+CODICECOSTO+SCAGLIONEDA+SCAGLIONEA+ANNI_DA+ANNI_A | Sempre |
| 6 | costiStandardFattispecie.csv | TMP_COSTI_STD_FATTISPECIE | SCARTI_TMP_COSTI_STD_FATTISPECIE | CODICEBANCA+CODICERAGGRUPPAMENTO+CODICECOSTO+SCAGLIONEDA+SCAGLIONEA+ANNI_DA+ANNI_A | Sempre |
| 7 | PAAMappatura.txt | TMP_PAAMAPPATURA | SCARTI_TMP_PAAMAPPATURA | CODICETITOLO+CODICE | BATCH_ENABLE_TASK_MAPPATURA |
| 8 | PAAMappaturaValutaria.txt | TMP_PAAMAPPATURAVALUTARIA | SCARTI_TMP_PAAMAPPATURAVALUTARIA | CODICETITOLO+CODICE | BATCH_ENABLE_TASK_MAPPATURAVALUTARIA |
| 9 | PAAMappaturaGeografica.txt | TMP_PAAMAPPATURAGEOGRAFICA | SCARTI_TMP_PAAMAPPATURAGEOGRAFICA | CODICETITOLO+CODICEITEM | BATCH_ENABLE_TASK_MAPPATURAGEOGRAFICA |
| 10 | PAAMappaturaSettoriale.txt | TMP_PAAMAPPATURASETTORIALE | SCARTI_TMP_PAAMAPPATURASETTORIALE | CODICETITOLO+CODICEITEM | BATCH_ENABLE_TASK_MAPPATURASETTORIALE |
| 11 | PAAScenaIndici.txt | TMP_PAASCENAINDICI | SCARTI_TMP_PAASCENAINDICI | ID_SCENARIO+CODICE_INDICE | BATCH_ENABLE_TASK_SCENAINDICI |
| 12 | ESGAttributes.csv | TMP_PPEESG_INSTR_ATTRIBUTES | SCARTI_TMP_PPEESG_INSTR_ATTR | INSTRUMENT_CODE+PILLAR_KEY | BATCH_ENABLE_TASK_ESG |
| 13 | anaStrumCoefficienti.csv | TMP_PPESTRUMCOEFF | SCARTI_TMP_PPESTRUMCOEFF | C_INSTRUMENT+C_CONTROLLO | BATCH_ENABLE_TASK_ANASTRUMCOEFFICIENTI |
| 14 | catalogoCanaliProdotto.csv | TMP_CATCANALIPRODOTTO | SCARTI_TMP_CATCANALIPRODOTTO | CODICEINTERNO+C_CANALE | BATCH_ENABLE_TASK_IMPORT_CANALE_DISTRIBUZIONE |

**Configurazione comune:** separatore `;`, header presente (skipFirstLine=TRUE), locale US, cleanTableMode=delete, maxNumberNoCommit=10000

---

## 1. PFPANATIT.csv — Anagrafica Titoli

**Tabella:** TMP_ANAGRTIT  
**File:** `PFPANATIT.csv`  
**strongFieldTypeCheck:** TRUE  
**N. campi:** 177  
**Campi obbligatori:** CODICEBANCA, CODICE_TITOLO, CODICE_RISCHIO, Z_STRUMENTO

**Note rispetto a BMED:**
- Campo 38: `CODE_TIPO_SOTTOSCRIZIONE` (VARCHAR 50) al posto di `IS_PAC` (JIRA 3347)
- Campo `IS_GRUPPO` posizionato dopo IS_CONFLITTO_INTERESSI
- Campo `Z_SOTTO_TIPO_BANCA` con max length 200 (vs 50 BMED)
- strongFieldTypeCheck = TRUE (più restrittivo)

Per il dettaglio completo dei 177 campi, vedere `procedure/README.md`.

---

## 2. TM_Actual.csv — Catalogo Target Market

**Tabella:** TMP_CATALOGOTM  
**File:** `TM_Actual.csv`

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICEBANCA | VARCHAR(50) | SI | Codice banca |
| 2 | MODSOMM | VARCHAR(50) | | Modalità somministrazione |
| 3 | CODICERISCHIO | VARCHAR(50) | SI | Codice strumento (FK PPECATALOGO) |
| 4 | TIPOCONTROLLO | VARCHAR(50) | SI | Tipo controllo TM |
| 5 | DOMINIO | INT | SI | Dominio del controllo |
| 6 | ESITO | VARCHAR(10) | SI | Esito (P=Positivo, N=Negativo) |

---

## 3. TM_Appoggio.csv — Setup Target Market

**Tabella:** TMP_SETUPTM  
**File:** `TM_Appoggio.csv`

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICEBANCA | VARCHAR(50) | SI | Codice banca |
| 2 | MODSOMM | VARCHAR(50) | SI | Modalità somministrazione |
| 3 | TIPOCONTROLLO | VARCHAR(50) | SI | Tipo controllo TM |
| 4 | ESITO | VARCHAR(10) | SI | Esito del controllo |
| 5 | ESITOCONTROLLO | VARCHAR(2) | SI | Codice esito (OK/KO) |
| 6 | MSGCONTROLLO | VARCHAR(200) | | Messaggio controllo |
| 7 | PRODUCT_TYPE | VARCHAR(50) | | Tipo prodotto |

---

## 4. TM_Fattispecie.csv — Fattispecie Target Market

**Tabella:** TMP_FATTISPECIETM  
**File:** `TM_Fattispecie.csv`

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICEBANCA | VARCHAR(50) | SI | Codice banca |
| 2 | RAGGRUPPAMENTO | VARCHAR(50) | SI | Fattispecie/raggruppamento |
| 3 | TIPOCONTROLLO | VARCHAR(50) | SI | Tipo controllo TM |
| 4 | DOMINIO | INT | SI | Dominio del controllo |
| 5 | ESITO | VARCHAR(10) | SI | Esito (P/N) |

---

## 5. costiStandardProdotto.csv — Costi Standard Prodotto

**Tabella:** TMP_COSTI_STD_PRODOTTO  
**File:** `costiStandardProdotto.csv`

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICEBANCA | VARCHAR(50) | SI | Codice banca |
| 2 | CODICEINTERNO | VARCHAR(50) | SI | Codice strumento |
| 3 | CODICEINTERNOAGGR | VARCHAR(50) | SI | Codice interno aggregazione |
| 4 | CODICEAGGREGAZIONE | VARCHAR(50) | SI | Codice aggregazione costo |
| 5 | CODICECOSTO | VARCHAR(50) | SI | Codice tipo costo |
| 6 | SCAGLIONEDA | DOUBLE | SI | Scaglione importo DA |
| 7 | SCAGLIONEA | DOUBLE | SI | Scaglione importo A |
| 8 | FREQUENZA | INT | | Frequenza applicazione |
| 9 | VALOREEURO | DOUBLE | | Valore costo in euro |
| 10 | VALOREPERC | DOUBLE | | Valore costo in % |
| 11 | VALOREMIN | DOUBLE | | Valore minimo |
| 12 | VALOREMAX | DOUBLE | | Valore massimo |
| 13 | IS_ATTIVO | VARCHAR(5) | | Flag attivo |
| 14 | IS_ESAUSTIVO | VARCHAR(5) | | Flag esaustivo |
| 15 | ANNI_DA | INT | SI | Anni detenzione DA |
| 16 | ANNI_A | INT | SI | Anni detenzione A |

---

## 6. costiStandardFattispecie.csv — Costi Standard Fattispecie

**Tabella:** TMP_COSTI_STD_FATTISPECIE  
**File:** `costiStandardFattispecie.csv`

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICEBANCA | VARCHAR(50) | SI | Codice banca |
| 2 | CODICERAGGRUPPAMENTO | VARCHAR(50) | SI | Codice fattispecie |
| 3 | CODICEAGGREGAZIONE | VARCHAR(50) | SI | Codice aggregazione |
| 4 | CODICECOSTO | VARCHAR(50) | SI | Codice tipo costo |
| 5 | SCAGLIONEDA | DOUBLE | SI | Scaglione DA |
| 6 | SCAGLIONEA | DOUBLE | SI | Scaglione A |
| 7 | FREQUENZA | INT | | Frequenza |
| 8 | VALOREEURO | DOUBLE | | Valore euro |
| 9 | VALOREPERC | DOUBLE | | Valore % |
| 10 | VALOREMIN | DOUBLE | | Valore minimo |
| 11 | VALOREMAX | DOUBLE | | Valore massimo |
| 12 | IS_ATTIVO | INT | | Flag attivo |
| 13 | ANNI_DA | INT | SI | Anni detenzione DA |
| 14 | ANNI_A | INT | SI | Anni detenzione A |

---

## 7. PAAMappatura.txt — Mappatura Asset Class

**Tabella:** TMP_PAAMAPPATURA  
**File:** `PAAMappatura.txt`  
**Condizione:** BATCH_ENABLE_TASK_MAPPATURA

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICETITOLO | VARCHAR(100) | SI | Codice strumento |
| 2 | CODICE | VARCHAR(100) | SI | Codice asset class/indice |
| 3 | PESO | DOUBLE | SI | Peso nella mappatura |
| 4 | BETA | DOUBLE | | Beta coefficiente |

---

## 8. PAAMappaturaValutaria.txt — Mappatura Valutaria

**Tabella:** TMP_PAAMAPPATURAVALUTARIA  
**File:** `PAAMappaturaValutaria.txt`  
**Condizione:** BATCH_ENABLE_TASK_MAPPATURAVALUTARIA

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICETITOLO | VARCHAR(100) | SI | Codice strumento |
| 2 | CODICE | VARCHAR(100) | SI | Codice valuta |
| 3 | PESO | DOUBLE | SI | Esposizione % alla valuta |

---

## 9. PAAScenaIndici.txt — Scenari Indici

**Tabella:** TMP_PAASCENAINDICI  
**File:** `PAAScenaIndici.txt`  
**Condizione:** BATCH_ENABLE_TASK_SCENAINDICI

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | ID_SCENARIO | INT | SI | Identificativo scenario |
| 2 | CODICE_INDICE | VARCHAR(50) | SI | Codice indice/asset class |
| 3 | VALUE | DOUBLE | SI | Rendimento scenario |

---

## 10. ESGAttributes.csv — Attributi ESG

**Tabella:** TMP_PPEESG_INSTR_ATTRIBUTES  
**File:** `ESGAttributes.csv`  
**Condizione:** BATCH_ENABLE_TASK_ESG

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | INSTRUMENT_CODE | VARCHAR(50) | SI | Codice strumento |
| 2 | PILLAR_KEY | VARCHAR(30) | SI | Chiave pillar (ESG, SE, TE, PAI_E, PAI_SG, ESG_OVERALL) |
| 3 | PARENT_PILLAR | VARCHAR(30) | | Pillar padre |
| 4 | SCORE | DOUBLE | | Score ESG |
| 5 | CLASS_CODE | INT | | Codice classe |
| 6 | IS_PILLAR_ACTIVE | INT | | Flag pillar attivo |
| 7 | RATING_PILLAR | VARCHAR(30) | | Rating pillar |
| 8 | PERC | DOUBLE | | Esposizione % |
| 9 | TS_AGGIORNAMENTO | INT | | Timestamp aggiornamento |
| 10 | MAX_PREF_ELIGIBLE | INT | | Max preferenza eligibile |

---

## 11. catalogoCommerciale.csv — Catalogo Commerciale

**Tabella:** TMP_CATALOGOCOMMERCIALE  
**File:** `catalogoCommerciale.csv`  
**Condizione:** BATCH_ENABLE_TASK_IMPORT_CATALOGOCOMMERCIALE

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICEBANCA | VARCHAR(50) | SI | Codice banca |
| 2 | C_SEGMENTO | VARCHAR(100) | SI | Codice segmento commerciale |
| 3 | CODICEINTERNO | VARCHAR(100) | SI | Codice strumento |
| 4 | D_INIZIO | INT | | Data inizio validità (YYYYMMDD) |
| 5 | D_FINE | INT | | Data fine validità (YYYYMMDD) |
| 6 | IS_AUTOMATICA | INT | | Flag inserimento automatico |
| 7 | TS_AGGIORNAMENTO | INT | | Timestamp aggiornamento |

---

## 12. govPraProxy.txt — PRA Proxy

**Tabella:** TMP_PPEPRAPROXY  
**File:** `govPraProxy.txt`  
**Condizione:** BATCH_ENABLE_TASK_IMPORT_PRAPROXY

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICE_TITOLO | VARCHAR(50) | SI | Codice strumento |
| 2 | ISIN | VARCHAR(50) | | ISIN |
| 3 | DESCRIZIONE | VARCHAR(200) | | Descrizione strumento |
| 4 | IDPROXYMKT | VARCHAR(50) | | ID proxy mercato |
| 5 | IDPROXYRC | VARCHAR(50) | | ID proxy rischio credito |
| 6 | TIPO | VARCHAR(50) | | Tipo strumento |
| 7 | TIPOVAL | VARCHAR(50) | | Tipo valutazione |
| 8 | BETA | DOUBLE | | Coefficiente beta |
| 9 | VOLRES | DOUBLE | | Volatilità residua |
| 10 | CLASSECOMPLESSITA | VARCHAR(50) | | Classe complessità |
| 11 | INDICATORELIQUIDITA | DOUBLE | | Indicatore liquidità |
| 12 | IS_ILLIQUIDO | INT | | Flag illiquido |
| 13 | TMDORIGPRIMARIO | DOUBLE | | TMD originale primario |
| 14 | TMDORIGSECONDARIO | DOUBLE | | TMD originale secondario |
| 15 | IS_PROXYMKT | INT | | Flag proxy mercato |
| 16 | IS_PROXYRX | INT | | Flag proxy RX |
| 17 | IS_PROXYTMD | INT | | Flag proxy TMD |
| 18 | PREVALEPROXY | VARCHAR(50) | | Quale proxy prevale |

---

## 13. eccezioni_switch.txt — Eccezioni Switch

**Tabella:** TMP_ECCEZIONISWITCH  
**File:** `eccezioni_switch.txt`  
**Condizione:** Sempre attivo

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICE_SICAV | VARCHAR(50) | SI | Codice SICAV/fondo |
| 2 | FAMIGLIA_IN | VARCHAR(50) | SI | Famiglia di partenza |
| 3 | FAMIGLIA_OUT | VARCHAR(50) | SI | Famiglia di destinazione |

---

## 14. anaStrumCoefficienti.csv — Coefficienti Strumento

**Tabella:** TMP_PPESTRUMCOEFF  
**File:** `anaStrumCoefficienti.csv`  
**Condizione:** BATCH_ENABLE_TASK_ANASTRUMCOEFFICIENTI (attualmente **disabilitato**)

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | C_INSTRUMENT | VARCHAR(50) | SI | Codice strumento |
| 2 | C_CONTROLLO | VARCHAR(50) | SI | Codice controllo |
| 3 | PERC | DOUBLE | SI | Percentuale/coefficiente |
| 4 | TS_AGGIORNAMENTO | INT | SI | Timestamp aggiornamento |

---

## 15. catalogoCanaliProdotto.csv — Canali Distribuzione

**Tabella:** TMP_CATCANALIPRODOTTO  
**File:** `catalogoCanaliProdotto.csv`  
**Condizione:** BATCH_ENABLE_TASK_IMPORT_CANALE_DISTRIBUZIONE (attualmente **disabilitato**)

| # | Campo | Tipo | Obbl. | Descrizione |
|---|-------|------|-------|-------------|
| 1 | CODICEINTERNO | VARCHAR(100) | SI | Codice strumento |
| 2 | C_CANALE | VARCHAR(50) | SI | Codice canale distribuzione |
| 3 | TS_AGGIORNAMENTO | INT | | Timestamp aggiornamento |
