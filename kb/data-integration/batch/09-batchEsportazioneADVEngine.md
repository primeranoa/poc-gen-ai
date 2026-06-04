# 09 — batchEsportazioneADVEngine.xml

**Job Name:** `ESPORTAZIONE ADV ENGINE`  
**Tipo:** SQL Export + Java

## Scopo

Esporta i dati dal database verso file CSV/XML/JSON per l'Advisory Engine runtime.

## File esportati

| # | File output | Formato | Tabelle fonte |
|---|-------------|---------|---------------|
| 1 | catalogoTitoli.csv | CSV | PPECATALOGO_EFFETTIVO_VIEW |
| 2 | soglieConcentrazioneComplessi.csv | CSV | PPECONCENTRAZIONE_CLASSESP |
| 3 | soglieConcentrazione.csv | CSV | PPECONCENTRAZIONEPO |
| 4 | soglieFrequenza.csv | CSV | PPESOGLIAFREQUENZAMODELLO |
| 5 | parametriSuitability.xml | XML | (Java) |
| 6 | parametriPPE.xml | XML | (Java) |
| 7 | ESGParameters.xml | XML | (Java) |
| 8 | scoreESG.json | JSON | (Java) |
| 9 | PAACatalogoTM.txt | CSV | PPECATALOGOTM + PPECATALOGO |
| 10 | PAACatalogoFattispecieTM.txt | CSV | PPEFATTISPECIETM |
| 11 | PAAParametriProdotti.txt | CSV | PPECATALOGO_EFFETTIVO_VIEW |
| 12 | costiStandardProdotto.csv | CSV | PPECOSTI |
| 13 | costiStandardFattispecie.csv | CSV | PPECOSTIFATTISPECIE |
| 14 | PAAMappatura.txt | CSV | PAAMAPPATURA |
| 15 | PAAMappaturaValutaria.txt | CSV | PAAMAPPATURAVALUTARIA |
| 16 | PAAScenaIndici.txt | CSV | PAASCENAINDICI |
| 17 | eccezioniSwitch.csv | CSV | PPEECCEZIONISWITCH |

## Classi Java utilizzate

| Classe | File generato |
|--------|---------------|
| `it.prometeia.ppegov.batch.EsportazioneParametri` | parametriSuitability.xml, parametriPPE.xml |
| `it.prometeia.ppegov.batch.EsportazioneParametriESG` | ESGParameters.xml |
| `it.prometeia.ppegov.batch.EsportazioneScoreESG` | scoreESG.json |
