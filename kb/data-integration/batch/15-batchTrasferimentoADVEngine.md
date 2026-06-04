# 15 — batchTrasferimentoADVEngine.xml

**Job Name:** `TRASFERIMENTO ADV ENGINE`  
**Tipo:** FileSystem

## Scopo

Trasferisce i file validati dall'area staging alla cartella di produzione dell'Advisory Engine. Deploy atomico.

## Task

### Task 0 — Pulizia area produzione

| Operazione | Path |
|-----------|------|
| Delete all | `%ADVE_HOME%/ini/*` |
| Delete all | `%ADVE_HOME%/importFile/*` |
| Create dir | Ricreazione cartelle vuote |

### Task 1 — Copia file

| Source | Pattern | Destination |
|--------|---------|-------------|
| `%ADVE_HOME_STAGING%/ini/` | `.*\.(txt|csv|xml|json)` | `%ADVE_HOME%/ini/` |
| `%ADVE_HOME_STAGING%/importFile/` | `.*\.(txt|csv)` | `%ADVE_HOME%/importFile/` |
