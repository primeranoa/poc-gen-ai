# 10 — batchCaricamentoInfoRischio.xml

**Job Name:** `Caricamento Info Rischio`  
**Tipo:** Java + SQL  
**Classe:** `it.prometeia.ppegov.batch.CaricamentoInfoRischio`

## Scopo

Calcola gli indicatori di rischio per tutti gli strumenti e aggiorna il catalogo.

## Mapping indicatori

| Campo PPEINFORISCHIO | Campo PPECATALOGO | Indicatore |
|---------------------|-------------------|------------|
| CVAR | RISCHIO_MERCATO | Conditional VaR |
| UL1Y | RISCHIOCREDITO | Unexpected Loss 1Y |
| INDLIQ | ISL | Indicatore liquidita |
| VAR | SRI | Value at Risk |
