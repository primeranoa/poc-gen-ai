# 14 — batchCheckEsportazioni.xml

**Job Name:** `CHECK ESPORTAZIONI`  
**Tipo:** Java  
**Classe:** `it.prometeia.ppegov.batch.CheckEsportazioni`

## Scopo

Valida i file esportati dai batch 09, 11, 12, 13, verificando che siano stati generati correttamente.

## Logica

- Verifica esistenza e non-vuotezza dei file nell'area staging
- Se un file e mancante o corrotto, il batch fallisce
