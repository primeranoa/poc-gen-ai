# 20 — batchPubblicaModificheACaldo.xml

**Job Name:** `PUBBLICA MODIFICHE A CALDO`  
**Tipo:** Java  
**Esecuzione:** On-demand (non in batchTotale)

## Scopo

Permette il deploy di modifiche alla configurazione senza eseguire l'intero ciclo batch notturno.

## Casi d'uso

- Disabilitazione/abilitazione di un prodotto
- Modifica soglie concentrazione
- Aggiornamento parametri ESG
- Modifica eccezioni switch

## Note

- Non fa parte del flusso standard batchTotale.sh
- Eseguibile su richiesta dall'operatore
- Esporta solo i file impattati dalla modifica
- Non esegue importazione/controlli/storicizzazione
