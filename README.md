# POC_GEN_AI — Proof of Concept AI-assisted Data Integration

Client POC per dimostrare l'uso di strumenti AI (Kiro / LLM) nel processo di data-integration ADVEngine/Governance.

## Struttura

```
POC_GEN_AI/
├── data-integration/       # Batch XML (importazione, update, controlli, esportazione)
│   ├── input/              # Cartella dove depositare i file CSV da importare
│   └── output/             # Cartella dove vengono generati i file di output
├── tracciati/              # Definizioni tracciato XML per l'importazione CSV
├── procedure/              # Script Python di conversione/trasformazione
│   └── converti_anatit_bmed_to_prompft.py
└── README.md
```

## Procedure disponibili

### `converti_anatit_bmed_to_prompft.py`

Converte un file `ANATIT.csv` nel formato BMED (165 colonne) in un file `PFPANATIT.csv` compatibile con il tracciato PROMPFT (177 colonne).

**Uso:**
```bash
python procedure/converti_anatit_bmed_to_prompft.py [input.csv] [output.csv]
```

Se non si specificano argomenti, lo script cerca `ANATIT.csv` nella stessa cartella e produce `PFPANATIT.csv`.

**Cosa fa:**
- Rinomina colonne con naming diverso (es. IS_COVERED_RISK → COVERED_RISK)
- Converte IS_PAC (0/1) → CODE_TIPO_SOTTOSCRIZIONE ("PAC"/"")
- Rimuove campi esclusivi BMED non presenti in PROMPFT
- Aggiunge colonne vuote per campi solo-PROMPFT
- Produce output con separatore `;` e header

## Tracciati (basati su PROMPFT)

I file XML nella cartella `tracciati/` definiscono la struttura attesa per l'importazione batch.
Il tracciato principale è `anagrtit.xml` (anagrafica titoli, 177 campi).

## Note

- La data-integration è una copia di quella PROMPFT (PostgreSQL)
- Il campo `C_PIR` non viene popolato dallo script (resta NULL) — comportamento atteso
- Il file CSV di input deve avere encoding UTF-8 e separatore `;`
