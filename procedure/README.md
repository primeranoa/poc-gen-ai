# Procedura Completa: Conversione Flussi BMED → PROMPFT

## Obiettivo

Trasformare i file CSV prodotti dalla data-integration **BMED** in file compatibili con l'importazione **PROMPFT**, permettendo di alimentare un ambiente PROMPFT con dati provenienti da BMED.

---

## Flussi Attivi in PROMPFT (analisi variabili d'ambiente)

### Configurazione da `ppebatch.ini`

| Variabile | Valore | Stato |
|-----------|--------|-------|
| `BATCH_ENABLE_TASK_ANASTRUMCOEFFICIENTI` | false | ❌ Disabilitato |
| `BATCH_ENABLE_TASK_CARICAMENTOCACHE_SQLDB` | false | ❌ Disabilitato |
| `BATCH_ENABLE_TASK_ESG_PARAMETERS_EXPORT` | true | ✅ Attivo |
| `BATCH_ENABLE_TASK_IMPORT_CANALE_DISTRIBUZIONE` | false | ❌ Disabilitato |
| `BATCH_ENABLE_TASK_EXPORT_PARAMETRI_SP` | true | ✅ Attivo |
| `BATCH_ENABLE_TASK_EXPORT_CAT` | true | ✅ Attivo |
| `BATCH_ENABLE_TASK_IMPORT_PRAPROXY` | true | ✅ Attivo |
| `BATCH_ENABLE_TASK_INFORISCHIO` | true | ✅ Attivo |
| `BATCH_ENABLE_TASK_MAPPATURAGEOGRAFICA` | false | ❌ Disabilitato |
| `BATCH_ENABLE_TASK_MAPPATURASETTORIALE` | false | ❌ Disabilitato |
| `BATCH_ENABLE_TASK_SCENAINDICIGREZZE` | false | ❌ Disabilitato |

### Variabili non in ppebatch.ini (abilitate per default dal container Docker)

| Variabile | Valore implicito | Stato |
|-----------|-----------------|-------|
| `BATCH_ENABLE_TASK_MAPPATURA` | true (default) | ✅ Attivo |
| `BATCH_ENABLE_TASK_MAPPATURAVALUTARIA` | true (default) | ✅ Attivo |
| `BATCH_ENABLE_TASK_SCENAINDICI` | true (default) | ✅ Attivo |
| `BATCH_ENABLE_TASK_ESG` | true (default) | ✅ Attivo |
| `BATCH_ENABLE_TASK_IMPORT_CATALOGOCOMMERCIALE` | true (default) | ✅ Attivo |
| `BATCH_ENABLE_TASK_ALLINEAMENTO_GIORNALIERO` | true (default) | ✅ Attivo |
| `BATCH_ENABLE_TASK_CARICAMENTOCACHE_REDIS` | true (default) | ✅ Attivo |
| `BATCH_ENABLE_TASK_CARICAMENTOCACHE_DYNAMODB` | true (default) | ✅ Attivo |

### File CSV effettivamente richiesti nella cartella `input/` (13 attivi, 5 disabilitati)

| # | File | Flusso | Stato | Prodotto da BMED? |
|---|------|--------|-------|-------------------|
| 1 | `PFPANATIT.csv` | Anagrafica titoli | ✅ Sempre attivo | ✅ Con script conversione |
| 2 | `TM_Actual.csv` | Catalogo TM | ✅ Sempre attivo | ✅ Diretto |
| 3 | `TM_Appoggio.csv` | Setup TM | ✅ Sempre attivo | ✅ Diretto |
| 4 | `TM_Fattispecie.csv` | Fattispecie TM | ✅ Sempre attivo | ✅ Rinomina file |
| 5 | `costiStandardProdotto.csv` | Costi prodotto | ✅ Sempre attivo | ✅ Diretto |
| 6 | `costiStandardFattispecie.csv` | Costi fattispecie | ✅ Sempre attivo | ✅ Diretto |
| 7 | `eccezioni_switch.txt` | Eccezioni switch | ✅ Sempre attivo | ❌ Non prodotto |
| 8 | `PAAMappatura.txt` | Mappatura asset class | ✅ Attivo (default) | ❌ Non prodotto |
| 9 | `PAAMappaturaValutaria.txt` | Mappatura valutaria | ✅ Attivo (default) | ❌ Non prodotto |
| 10 | `PAAScenaIndici.txt` | Scenari indici | ✅ Attivo (default) | ❌ Non prodotto |
| 11 | `ESGAttributes.csv` | Attributi ESG | ✅ Attivo (default) | ✅ Diretto |
| 12 | `catalogoCommerciale.csv` | Catalogo commerciale | ✅ Attivo (default) | ❌ Non prodotto |
| 13 | `govPraProxy.txt` | PRA Proxy | ✅ Attivo (ini=true) | ❌ Non prodotto |
| 14 | `PAAMappaturaGeografica.txt` | Mappatura geografica | ❌ Disabilitato | — |
| 15 | `PAAMappaturaSettoriale.txt` | Mappatura settoriale | ❌ Disabilitato | — |
| 16 | `PAAScenaIndiciGrezze.txt` | Scenari grezzi | ❌ Disabilitato | — |
| 17 | `anaStrumCoefficienti.csv` | Coefficienti strumento | ❌ Disabilitato | — |
| 18 | `catalogoCanaliProdotto.csv` | Canali distribuzione | ❌ Disabilitato | — |

### Copertura BMED

- **7 flussi su 13** attivi sono coperti da BMED (direttamente o con conversione)
- **6 flussi** attivi non sono prodotti da BMED e dovranno essere forniti separatamente o disabilitati nel POC

---

## Analisi Comparativa Tracciati

### Riepilogo Compatibilita

| # | Tracciato | File BMED | File PROMPFT | Compatibilita | Azione |
|---|-----------|-----------|--------------|---------------|--------|
| 1 | ANAGRTIT | `ANATIT.csv` | `PFPANATIT.csv` | ⚠️ Trasformazione | Script Python |
| 2 | CATALOGOTM | `TM_Actual.csv` | `TM_Actual.csv` | ✅ Compatibile | Nessuna |
| 3 | SETUPTM | `TM_Appoggio.csv` | `TM_Appoggio.csv` | ✅ Identico | Nessuna |
| 4 | FATTISPECIETM | `CATALOGOTMFATTISPECIE.csv` | `TM_Fattispecie.csv` | ✅ Compatibile | Rinomina file |
| 5 | ESG | `ESGAttributes.csv` | `ESGAttributes.csv` | ✅ Identico | Nessuna |
| 6 | COSTI_STD_PRODOTTO | `costiStandardProdotto.csv` | `costiStandardProdotto.csv` | ✅ Compatibile | Nessuna |
| 7 | COSTI_STD_FATTISPECIE | `costiStandardFattispecie.csv` | `costiStandardFattispecie.csv` | ✅ Compatibile | Nessuna |
| 8 | SCORE_PICKING | `ScorePicking.csv` | — | ❌ Solo BMED | Non applicabile |

---

## 1. ANAGRTIT — Anagrafica Titoli (Trasformazione necessaria)

### Metadati

| | BMED | PROMPFT |
|--|------|---------|
| File input | `ANATIT.csv` | `PFPANATIT.csv` |
| N. colonne | 165 | 177 |
| strongFieldTypeCheck | Disabilitato | **TRUE** |
| Separatore | `;` | `;` |
| Header | Si | Si |

### Rinomina colonne (16 campi)

| # | Nome BMED (CSV) | Nome PROMPFT | Nota |
|---|-----------------|--------------|------|
| 1 | `IS_PAC` | `CODE_TIPO_SOTTOSCRIZIONE` | Anche cambio tipo: INT → VARCHAR |
| 2 | `IS_COVERED_RISK` | `COVERED_RISK` | Prefisso IS_ rimosso |
| 3 | `IS_COVERED_AC` | `COVERED_AC` | Prefisso IS_ rimosso |
| 4 | `IS_COVERED_CURR_EXP` | `COVERED_CURR_EXP` | Prefisso IS_ rimosso |
| 5 | `IS_COVERED_HS_HNWI` | `COVERED_HS_HNWI` | Prefisso IS_ rimosso |
| 6 | `IS_COVERED_STRESS` | `COVERED_STRESS` | Prefisso IS_ rimosso |
| 7 | `IS_CORE_LIST_CONSULBASE` | `CORE_LIST_CONSULBASE` | Prefisso IS_ rimosso |
| 8 | `IS_CORE_LIST_CONSULPRIV` | `CORE_LIST_CONSULPRIV` | Prefisso IS_ rimosso |
| 9 | `IS_PERIMETRO_REND` | `PERIMETRO_REND` | Prefisso IS_ rimosso |
| 10 | `IS_PRESENZA_DOC` | `PRESENZA_DOC` | Prefisso IS_ rimosso |
| 11 | `IS_HAS_SOTTOSTANTI` | `HAS_SOTTOSTANTI` | Prefisso IS_ rimosso |
| 12 | `IS_COMBINAZIONEFISSA` | `IS_COMBINAZIONE_FISSA` | Underscore aggiunto |
| 13 | `COSTO_SOSTENIBILE_ANNUO` | `COSTO_SOSTENIBILE_ANNO` | Suffisso troncato |
| 14 | `ISCATALOGOCOMM` | `IS_CATALOGOCOMM` | Underscore aggiunto |
| 15 | `IS_EM_GRUPPO` | `IS_GRUPPO` | Semplificato |
| 16 | `IS_ESG` | `IS_ESG_APPLICABLE` | Suffisso aggiunto |

### Trasformazione valori

| Campo BMED | Valore BMED | Campo PROMPFT | Valore PROMPFT |
|------------|-------------|---------------|----------------|
| `IS_PAC` | `1` | `CODE_TIPO_SOTTOSCRIZIONE` | `PAC` |
| `IS_PAC` | `0` o vuoto | `CODE_TIPO_SOTTOSCRIZIONE` | (vuoto) |

### Campi BMED rimossi (7 campi)

| Campo | Tipo | Motivo |
|-------|------|--------|
| `IS_EM_BANCA` | INT | Specifico BMED, non esiste in PROMPFT |
| `C_RAGGR_TITOLI` | VARCHAR(50) | Specifico BMED |
| `Z_RAGGR_TITOLI` | VARCHAR(50) | Specifico BMED |
| `PERC_CONCENTRAZIONE` | DOUBLE | Specifico BMED |
| `IS_ESG_W2` | INT | Secondo flag ESG, solo BMED |
| `IS_SOGGETTO_RATING` | INT | Specifico BMED |
| `IS_SOGGETTO_ISSUER` | INT | Specifico BMED |

### Campi aggiunti vuoti per PROMPFT (19 campi)

| Campo | Tipo | Descrizione |
|-------|------|-------------|
| `Z_STRUMENTO_BREVE` | VARCHAR(250) | Descrizione breve strumento |
| `IS_LOAD` | INT | Flag load |
| `IS_PINL` | INT | Flag PINL |
| `IS_COMPARABLE` | INT | Flag comparabile |
| `MIN_HP` | DOUBLE | Holding period minimo |
| `C_CAT_MORNINGSTAR` | VARCHAR(250) | Categoria Morningstar |
| `IS_PIR_ALTERNATIVE` | INT | Flag PIR alternativo |
| `IS_ELTIF` | INT | Flag ELTIF |
| `IS_FIA` | INT | Flag FIA |
| `IS_Q_UCTS` | INT | Flag quotato UCITS |
| `IS_Q_FIA` | INT | Flag quotato FIA |
| `IS_HEDGED` | INT | Flag hedged |
| `DEFAULTTMGROUP` | VARCHAR(50) | Gruppo TM default |
| `DEFAULTCOSTGROUP` | VARCHAR(50) | Gruppo costi default |
| `IS_RIMBORSI_PROGRAMMATI` | INT | Flag rimborsi programmati |
| `EXPERIENCE_GROUP_CODE` | VARCHAR(50) | Codice gruppo esperienza |
| `LOTTO_MIN_COMM` | DOUBLE | Lotto minimo commerciale |
| `LOTTO_MIN_SUCC_COMM` | DOUBLE | Lotto minimo successivo commerciale |
| `MOD_VERS_COMM` | INTEGER | Modalita versamento commerciale |

### Differenze tipo/lunghezza campi comuni

| Campo | BMED | PROMPFT | Impatto |
|-------|------|---------|---------|
| `C_TIPO_STRUMENTO_2` | VARCHAR(50) | VARCHAR(100) | Nessuno (PROMPFT accetta di piu) |
| `Z_SOTTO_TIPO_BANCA` | VARCHAR(50) | VARCHAR(200) | Nessuno |
| `TIPO_PAC` | VARCHAR(5) | VARCHAR(50) | Nessuno |
| `IS_ESG_APPLICABLE` | INT obbligatorio | INT opzionale | Nessuno |

### Campo C_PIR

Il campo `C_PIR` esiste sulla tabella DB `tmp_anagrtit` di PROMPFT ma **non** e nel tracciato XML. Viene usato nella query di UPDATE (batchUpdate.xml). Poiche non e nel tracciato, non viene popolato dall'importazione CSV e resta **NULL**. Comportamento atteso, nessuna azione necessaria.

---

## 2. CATALOGOTM — Catalogo Target Market

| # | Campo | Tipo | BMED obbl. | PROMPFT obbl. |
|---|-------|------|-----------|--------------|
| 1 | CODICEBANCA | VARCHAR(50) | ✅ | ✅ |
| 2 | MODSOMM | VARCHAR(50) | ✅ | ❌ |
| 3 | CODICERISCHIO | VARCHAR(50) | ✅ | ✅ |
| 4 | TIPOCONTROLLO | VARCHAR(50) | ✅ | ✅ |
| 5 | DOMINIO | INT | ✅ | ✅ |
| 6 | ESITO | VARCHAR(10) | ✅ | ✅ |

**Unica differenza:** MODSOMM e obbligatorio in BMED, opzionale in PROMPFT.
**Azione:** Nessuna. Il file `TM_Actual.csv` di BMED e direttamente importabile.

---

## 3. SETUPTM — Setup Target Market

| # | Campo | Tipo | Obbl. |
|---|-------|------|-------|
| 1 | CODICEBANCA | VARCHAR(50) | ✅ |
| 2 | MODSOMM | VARCHAR(50) | ✅ |
| 3 | TIPOCONTROLLO | VARCHAR(50) | ✅ |
| 4 | ESITO | VARCHAR(10) | ✅ |
| 5 | ESITOCONTROLLO | VARCHAR(2) | ✅ |
| 6 | MSGCONTROLLO | VARCHAR(200) | ❌ |
| 7 | PRODUCT_TYPE | VARCHAR(50) | ❌ |

**Azione:** Nessuna. Tracciati perfettamente identici.

---

## 4. FATTISPECIETM — Fattispecie Target Market

| # | Campo | Tipo | Obbl. |
|---|-------|------|-------|
| 1 | CODICEBANCA | VARCHAR(50) | ✅ |
| 2 | RAGGRUPPAMENTO | VARCHAR(50) | ✅ |
| 3 | TIPOCONTROLLO | VARCHAR(50) | ✅ |
| 4 | DOMINIO | INT | ✅ |
| 5 | ESITO | VARCHAR(10) | ✅ |

**Unica differenza:** il nome del file.
- BMED: `CATALOGOTMFATTISPECIE.csv`
- PROMPFT: `TM_Fattispecie.csv`

**Azione:** Rinominare il file:
```bash
cp CATALOGOTMFATTISPECIE.csv TM_Fattispecie.csv
```

---

## 5. ESG — Attributi ESG

| # | Campo | Tipo | Obbl. |
|---|-------|------|-------|
| 1 | INSTRUMENT_CODE | VARCHAR(50) | ✅ |
| 2 | PILLAR_KEY | VARCHAR(30) | ✅ |
| 3 | PARENT_PILLAR | VARCHAR(30) | ❌ |
| 4 | SCORE | DOUBLE | ❌ |
| 5 | CLASS_CODE | INT | ❌ |
| 6 | IS_PILLAR_ACTIVE | INT | ❌ |
| 7 | RATING_PILLAR | VARCHAR(30) | ❌ |
| 8 | PERC | DOUBLE | ❌ |
| 9 | TS_AGGIORNAMENTO | INT | ❌ |
| 10 | MAX_PREF_ELIGIBLE | INT | ❌ |

**Azione:** Nessuna. File identico.

---

## 6. COSTI_STD_PRODOTTO — Costi Standard Prodotto

| # | Campo | Tipo | BMED obbl. | PROMPFT obbl. |
|---|-------|------|-----------|--------------|
| 1 | CODICEBANCA | VARCHAR(50) | ✅ | ✅ |
| 2 | CODICEINTERNO | VARCHAR(50) | ✅ | ✅ |
| 3 | CODICEINTERNOAGGR | VARCHAR(50) | ✅ | ✅ |
| 4 | CODICEAGGREGAZIONE | VARCHAR(50) | ✅ | ✅ |
| 5 | CODICECOSTO | VARCHAR(50) | ✅ | ✅ |
| 6 | SCAGLIONEDA | DOUBLE | ❌ | ✅ |
| 7 | SCAGLIONEA | DOUBLE | ❌ | ✅ |
| 8 | FREQUENZA | INT | ❌ | ❌ |
| 9 | VALOREEURO | DOUBLE | ❌ | ❌ |
| 10 | VALOREPERC | DOUBLE | ❌ | ❌ |
| 11 | VALOREMIN | DOUBLE | ❌ | ❌ |
| 12 | VALOREMAX | DOUBLE | ❌ | ❌ |
| 13 | IS_ATTIVO | VARCHAR(5) | ✅ | ❌ |
| 14 | IS_ESAUSTIVO | VARCHAR(5) | ✅ | ❌ |
| 15 | ANNI_DA | INT | ✅ | ✅ |
| 16 | ANNI_A | INT | ✅ | ✅ |

**Azione:** Nessuna. BMED fornisce sempre tutti i campi.

---

## 7. COSTI_STD_FATTISPECIE — Costi Standard Fattispecie

| # | Campo | Tipo BMED | Tipo PROMPFT | BMED obbl. | PROMPFT obbl. |
|---|-------|-----------|--------------|-----------|--------------|
| 1 | CODICEBANCA | VARCHAR(50) | VARCHAR(50) | ✅ | ✅ |
| 2 | CODICERAGGRUPPAMENTO | VARCHAR(50) | VARCHAR(50) | ✅ | ✅ |
| 3 | CODICEAGGREGAZIONE | VARCHAR(50) | VARCHAR(50) | ✅ | ✅ |
| 4 | CODICECOSTO | VARCHAR(50) | VARCHAR(50) | ✅ | ✅ |
| 5 | SCAGLIONEDA | DOUBLE | DOUBLE | ❌ | ✅ |
| 6 | SCAGLIONEA | DOUBLE | DOUBLE | ❌ | ✅ |
| 7 | FREQUENZA | INT | INT | ❌ | ❌ |
| 8 | VALOREEURO | DOUBLE | DOUBLE | ❌ | ❌ |
| 9 | VALOREPERC | DOUBLE | DOUBLE | ❌ | ❌ |
| 10 | VALOREMIN | DOUBLE | DOUBLE | ❌ | ❌ |
| 11 | VALOREMAX | DOUBLE | DOUBLE | ❌ | ❌ |
| 12 | IS_ATTIVO | **VARCHAR(5)** | **INT** | ✅ | ❌ |
| 13 | ANNI_DA | INT | INT | ✅ | ✅ |
| 14 | ANNI_A | INT | INT | ✅ | ✅ |

**Differenza tipo IS_ATTIVO:** BMED manda VARCHAR ("0"/"1"), PROMPFT attende INT. PostgreSQL gestisce il cast implicito senza errori.
**Azione:** Nessuna.

---

## 8. SCORE_PICKING — Solo BMED

Tracciato esclusivo BMED con 7 campi (CODICE_TITOLO, SCORE_HFB, CODE_SILOS, DESC_SILOS, MICRO_AC, MACRO_AC, DATARIFERIMENTO). Non esiste equivalente in PROMPFT.
**Azione:** Non applicabile. Ignorare.

---

## Istruzioni Operative

### Prerequisiti

- Python 3.6+
- File CSV da BMED (encoding UTF-8, separatore `;`)

### Esecuzione completa

```bash
# 1. Converti anagrafica titoli (unica trasformazione reale)
python procedure/converti_anatit_bmed_to_prompft.py ANATIT.csv PFPANATIT.csv

# 2. Rinomina fattispecie TM
cp CATALOGOTMFATTISPECIE.csv TM_Fattispecie.csv

# 3. Gli altri file sono direttamente compatibili (copiare nella cartella input):
#    - TM_Actual.csv              → usare cosi com'e
#    - TM_Appoggio.csv            → usare cosi com'e
#    - ESGAttributes.csv          → usare cosi com'e
#    - costiStandardProdotto.csv  → usare cosi com'e
#    - costiStandardFattispecie.csv → usare cosi com'e

# 4. Flussi attivi in PROMPFT ma non prodotti da BMED (da fornire separatamente):
#    - PAAMappatura.txt
#    - PAAMappaturaValutaria.txt
#    - PAAScenaIndici.txt
#    - catalogoCommerciale.csv
#    - govPraProxy.txt
#    - eccezioni_switch.txt
```

### Output atteso

Dopo la conversione, i file risultanti sono importabili dalla data-integration PROMPFT (batchImportazione.xml → batchControlliPreliminari.xml → batchUpdate.xml) senza errori.

Il campo `C_PIR` restera NULL nel DB — comportamento atteso.

---

## Verifiche eseguite

La compatibilita e stata verificata analizzando:
1. **batchImportazione.xml** — importazione multithread legge il CSV tramite il tracciato XML
2. **batchControlliPreliminari.xml** — controllo duplicati e FK su `tmp_anagrtit`
3. **batchUpdate.xml** — INSERT INTO PPECATALOGO con SELECT da `tmp_anagrtit`
4. **batchCheckFlussiInput.xml** — verifica esistenza file `PFPANATIT.csv`
5. **Schema DB** (`tmp_anagrtit` su PostgreSQL BPM svil) — tutte le colonne referenziate nelle query sono presenti o nullable
6. **ppebatch.ini** — variabili BATCH_ENABLE_TASK per determinare flussi attivi/disattivi
