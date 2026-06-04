# 09 — batchEsportazioneADVEngine.xml

**Job Name:** `ESPORTAZIONE ADV ENGINE`  
**Tipo:** SQL Export + Java

## Scopo

Esporta i dati dal database verso file CSV/XML/JSON per l'Advisory Engine runtime.

## File esportati

| # | File output | Formato | Destinazione |
|---|-------------|---------|-------------|
| 1 | catalogoTitoli.csv | CSV | ini/ |
| 2 | soglieConcentrazioneComplessi.csv | CSV | ini/ |
| 3 | soglieConcentrazione.csv | CSV | ini/ |
| 4 | soglieFrequenza.csv | CSV | ini/ |
| 5 | parametriSuitability.xml | XML | ini/ |
| 6 | parametriPPE.xml | XML | ini/ |
| 7 | ESGParameters.xml | XML | ini/ |
| 8 | scoreESG.json | JSON | ini/ |
| 9 | PAACatalogoTM.txt | CSV | importFile/ |
| 10 | PAACatalogoFattispecieTM.txt | CSV | importFile/ |
| 11 | PAAParametriProdotti.txt | CSV | importFile/ |
| 12 | costiStandardProdotto.csv | CSV | ini/ |
| 13 | costiStandardFattispecie.csv | CSV | ini/ |
| 14 | PAAMappatura.txt | CSV | importFile/ |
| 15 | PAAMappaturaValutaria.txt | CSV | importFile/ |
| 16 | PAAScenaIndici.txt | CSV | importFile/ |
| 17 | eccezioniSwitch.csv | CSV | ini/ |
