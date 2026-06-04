# 17 — batchAllineamentoGiornaliero.xml

**Job Name:** `ALLINEAMENTO GIORNALIERO`  
**Tipo:** SQL  
**Ambito Applicativo:** 2

## Scopo

Allinea i dati per l'Ambito Applicativo 2 con le modifiche del giorno effettuate su AA=1.

## Logica

- Eseguito dopo tutti i batch AA=1
- Sincronizza le tabelle tra AA=1 e AA=2
- Allinea: catalogo, configurazioni, parametri modificati
- Permette all'AA=2 di operare con dati aggiornati
