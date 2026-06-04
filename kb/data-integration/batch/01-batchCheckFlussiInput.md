# 01 — batchCheckFlussiInput.xml

**Job Name:** `FASE CHECK FLUSSI INPUT`  
**Tipo:** Java  
**Classe:** `it.prometeia.ppegov.batch.CheckFlussiInput`

## Scopo

Verifica l'esistenza fisica dei file CSV/TXT richiesti per l'importazione. Se un file obbligatorio manca, il batch fallisce e l'intera catena si interrompe.

## Task

### Task 0 — File obbligatori (sempre verificati)

| # | File | Descrizione |
|---|------|-------------|
| 1 | `PFPANATIT.csv` | Anagrafica prodotti |
| 2 | `costiStandardProdotto.csv` | Costi standard per prodotto |
| 3 | `costiStandardFattispecie.csv` | Costi standard per fattispecie |
| 4 | `TM_Actual.csv` | Catalogo Target Market |
| 5 | `TM_Appoggio.csv` | Setup Target Market |
| 6 | `TM_Fattispecie.csv` | Fattispecie Target Market |

### Task 1 — Catalogo commerciale (condizionale)
**Flag:** `BATCH_ENABLE_TASK_IMPORT_CATALOGOCOMMERCIALE`  
**File:** `catalogoCommerciale.csv`

### Task 2 — Mappatura (condizionale)
**Flag:** `BATCH_ENABLE_TASK_MAPPATURA`  
**File:** `PAAMappatura.txt`

### Task 3 — Mappatura valutaria (condizionale)
**Flag:** `BATCH_ENABLE_TASK_MAPPATURAVALUTARIA`  
**File:** `PAAMappaturaValutaria.txt`

### Task 4 — Mappatura geografica (condizionale)
**Flag:** `BATCH_ENABLE_TASK_MAPPATURAGEOGRAFICA`  
**File:** `PAAMappaturaGeografica.txt`

### Task 5 — Mappatura settoriale (condizionale)
**Flag:** `BATCH_ENABLE_TASK_MAPPATURASETTORIALE`  
**File:** `PAAMappaturaSettoriale.txt`

### Task 6 — Scenari indici (condizionale)
**Flag:** `BATCH_ENABLE_TASK_SCENAINDICI`  
**File:** `PAAScenaIndici.txt`

### Task 7 — Scenari indici grezzi (condizionale)
**Flag:** `BATCH_ENABLE_TASK_SCENAINDICIGREZZE`  
**File:** `PAAScenaIndici.txt`

### Task 8 — ESG (condizionale)
**Flag:** `BATCH_ENABLE_TASK_ESG`  
**File:** `ESGAttributes.csv`

### Task 9 — PRA Proxy (condizionale)
**Flag:** `BATCH_ENABLE_TASK_IMPORT_PRAPROXY`  
**File:** `govPraProxy.txt`

### Task 10 — Coefficienti strumenti (condizionale)
**Flag:** `BATCH_ENABLE_TASK_ANASTRUMCOEFFICIENTI`  
**File:** `anaStrumCoefficienti.csv`
