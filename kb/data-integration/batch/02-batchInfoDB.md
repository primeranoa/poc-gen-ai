# 02 — batchInfoDB.xml

**Job Name:** `InfoDB`  
**Tipo:** Java  
**Classe:** `it.prometeia.ppegov.batch.InfoDB`

## Scopo

Recupera e logga informazioni sulla versione dello schema database installato.

## Task

### Task 0 — InfoDB

| Tipo | Classe Java |
|------|-------------|
| javaProcess | `it.prometeia.ppegov.batch.InfoDB` |

**Logica:**
- Legge la tabella `PPESCHEMAVERSION` per verificare la versione corrente dello schema
- Logga la versione a scopo di tracciabilita

**Tabelle coinvolte:** `PPESCHEMAVERSION` (lettura)
