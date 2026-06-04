
# Confronto Tracciati BMED vs PROMPFT

Analisi comparativa di tutti i tracciati XML condivisi tra i due clienti.

---

## 1. ANAGRTIT (Anagrafica Titoli)

| Attributo | BMED | PROMPFT |
|-----------|------|---------|
| File input | `ANATIT.csv` | `PFPANATIT.csv` |
| N. colonne | 165 | 177 |
| strongFieldTypeCheck | Disabilitato (commentato) | **TRUE** |

### Differenze strutturali

| # | Tipo differenza | BMED | PROMPFT | Note |
|---|----------------|------|---------|------|
| 1 | Rinomina + cambio tipo | `IS_PAC` (INT) | `CODE_TIPO_SOTTOSCRIZIONE` (VARCHAR 50) | Conversione: 1->"PAC", 0->"" |
| 2 | Rinomina header CSV | `IS_COVERED_RISK` | `COVERED_RISK` | Stesso dato |
| 3 | Rinomina header CSV | `IS_COVERED_AC` | `COVERED_AC` | Stesso dato |
| 4 | Rinomina header CSV | `IS_COVERED_CURR_EXP` | `COVERED_CURR_EXP` | Stesso dato |
| 5 | Rinomina header CSV | `IS_COVERED_HS_HNWI` | `COVERED_HS_HNWI` | Stesso dato |
| 6 | Rinomina header CSV | `IS_COVERED_STRESS` | `COVERED_STRESS` | Stesso dato |
| 7 | Rinomina header CSV | `IS_CORE_LIST_CONSULBASE` | `CORE_LIST_CONSULBASE` | Stesso dato |
| 8 | Rinomina header CSV | `IS_CORE_LIST_CONSULPRIV` | `CORE_LIST_CONSULPRIV` | Stesso dato |
| 9 | Rinomina header CSV | `IS_PERIMETRO_REND` | `PERIMETRO_REND` | Stesso dato |
| 10 | Rinomina header CSV | `IS_PRESENZA_DOC` | `PRESENZA_DOC` | Stesso dato |
| 11 | Rinomina header CSV | `IS_HAS_SOTTOSTANTI` | `HAS_SOTTOSTANTI` | Stesso dato |
| 12 | Rinomina header CSV | `IS_COMBINAZIONEFISSA` | `IS_COMBINAZIONE_FISSA` | Underscore aggiunto |
| 13 | Rinomina header CSV | `COSTO_SOSTENIBILE_ANNUO` | `COSTO_SOSTENIBILE_ANNO` | Troncato |
| 14 | Rinomina header CSV | `ISCATALOGOCOMM` | `IS_CATALOGOCOMM` | Underscore aggiunto |
| 15 | Rinomina header CSV | `IS_EM_GRUPPO` | `IS_GRUPPO` | Semplificato |
| 16 | Rinomina header CSV | `IS_ESG` | `IS_ESG_APPLICABLE` | Esteso |

### Campi BMED esclusi (non in PROMPFT)

| Campo | Tipo | Note |
|-------|------|------|
| `IS_EM_BANCA` | INT | Specifico BMED |
| `C_RAGGR_TITOLI` | VARCHAR(50) | Specifico BMED |
| `Z_RAGGR_TITOLI` | VARCHAR(50) | Specifico BMED |
| `PERC_CONCENTRAZIONE` | DOUBLE | Specifico BMED |
| `IS_ESG_W2` | INT | Secondo flag ESG (solo BMED) |
| `IS_SOGGETTO_RATING` | INT | Specifico BMED |
| `IS_SOGGETTO_ISSUER` | INT | Specifico BMED |

### Campi solo PROMPFT (assenti in BMED, valorizzati vuoti nella conversione)

| Campo | Tipo | Note |
|-------|------|------|
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

### Differenze tipo/lunghezza su campi comuni

| Campo | BMED | PROMPFT |
|-------|------|---------|
| `C_TIPO_STRUMENTO_2` | VARCHAR(50) | VARCHAR(100) |
| `Z_SOTTO_TIPO_BANCA` | VARCHAR(50) | VARCHAR(200) |
| `TIPO_PAC` | VARCHAR(5) | VARCHAR(50) |
| `IS_ESG_APPLICABLE` | INT, obbligatorio | INT, opzionale |

---

## 2. CATALOGOTM (Catalogo Target Market)

| Attributo | BMED | PROMPFT |
|-----------|------|---------|
| File input | `TM_Actual.csv` | `TM_Actual.csv` |
| N. colonne | 6 | 6 |

### Differenze

| Campo | BMED | PROMPFT |
|-------|------|---------|
| `MODSOMM` | obligatory=TRUE | obligatory non specificato (false) |

**Conclusione:** File BMED compatibile con PROMPFT senza modifiche.

---

## 3. SETUPTM (Setup Target Market)

| Attributo | BMED | PROMPFT |
|-----------|------|---------|
| File input | `TM_Appoggio.csv` | `TM_Appoggio.csv` |
| N. colonne | 7 | 7 |

**Conclusione:** Identici. File BMED direttamente importabile senza modifiche.

---

## 4. FATTISPECIETM (Fattispecie Target Market)

| Attributo | BMED | PROMPFT |
|-----------|------|---------|
| File input | `CATALOGOTMFATTISPECIE.csv` | `TM_Fattispecie.csv` |
| N. colonne | 5 | 5 |

### Differenze

| Tipo | BMED | PROMPFT |
|------|------|---------|
| Nome file | `CATALOGOTMFATTISPECIE.csv` | `TM_Fattispecie.csv` |

**Conclusione:** Struttura identica. Solo rinomina file necessaria.

---

## 5. ESG (Attributi ESG)

| Attributo | BMED | PROMPFT |
|-----------|------|---------|
| File input | `ESGAttributes.csv` | `ESGAttributes.csv` |
| N. colonne | 10 | 10 |

**Conclusione:** Identici. Nessuna modifica necessaria.

---

## 6. COSTI_STD_PRODOTTO (Costi Standard Prodotto)

| Attributo | BMED | PROMPFT |
|-----------|------|---------|
| File input | `costiStandardProdotto.csv` | `costiStandardProdotto.csv` |
| N. colonne | 16 | 16 |

### Differenze

| Campo | BMED | PROMPFT |
|-------|------|---------|
| `SCAGLIONEDA` | obligatory=FALSE | obligatory=TRUE |
| `SCAGLIONEA` | obligatory=FALSE | obligatory=TRUE |
| `IS_ATTIVO` | obligatory=TRUE | obligatory=FALSE |
| `IS_ESAUSTIVO` | obligatory=TRUE | obligatory=FALSE |

**Conclusione:** Compatibile. Nessuna trasformazione necessaria.

---

## 7. COSTI_STD_FATTISPECIE (Costi Standard Fattispecie)

| Attributo | BMED | PROMPFT |
|-----------|------|---------|
| File input | `costiStandardFattispecie.csv` | `costiStandardFattispecie.csv` |
| N. colonne | 14 | 14 |

### Differenze

| Campo | BMED | PROMPFT |
|-------|------|---------|
| `SCAGLIONEDA` | obligatory=FALSE | obligatory=TRUE |
| `SCAGLIONEA` | obligatory=FALSE | obligatory=TRUE |
| `IS_ATTIVO` | VARCHAR(5) obbl. | INT opzionale |

**Conclusione:** Compatibile (PostgreSQL cast implicito VARCHAR->INT).

---

## 8. SCORE_PICKING (Solo BMED)

Tracciato esclusivo BMED. Non ha equivalente in PROMPFT.

---

## Riepilogo

| Tracciato | Compatibilita | Azione |
|-----------|---------------|--------|
| **ANAGRTIT** | Trasformazione | Script Python |
| **CATALOGOTM** | Compatibile | Nessuna |
| **SETUPTM** | Identico | Nessuna |
| **FATTISPECIETM** | Compatibile | Rinomina file |
| **ESG** | Identico | Nessuna |
| **COSTI_STD_PRODOTTO** | Compatibile | Nessuna |
| **COSTI_STD_FATTISPECIE** | Compatibile | Nessuna |
| **SCORE_PICKING** | Solo BMED | Non applicabile |
