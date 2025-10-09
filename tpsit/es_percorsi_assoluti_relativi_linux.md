# Esercizio Percorsi Assoluti e Relativi - Linux Shell

## Setup Iniziale
Crea all'interno della cartella **Progetti** il seguente albero di directory:

```
Progetti/
├── laboratorio/
│   ├── codice/
│   │   └── src/
│   ├── documenti/
│   └── test/
├── backup/
│   ├── settimanale/
│   └── mensile/
└── archivio/
    ├── 2024/
    │   ├── gennaio/
    │   └── febbraio/
    └── 2025/
```

Successivamente, posizionati nella cartella **codice** e crea con l'editor nano il file **script.sh**.

---

## PRIMA PARTE: Path Assoluti

Usa **esclusivamente path assoluti** per tutti gli esercizi seguenti.

1. Sei nella directory **codice**. Copia script.sh nella directory **src**.

2. Sei nella directory **test**. Copia script.sh dalla directory **codice** alla directory **documenti**.

3. Sei nella directory **gennaio**. Copia script.sh dalla directory **codice** alla directory **settimanale**.

4. Sei nella directory **backup**. Copia script.sh dalla directory **codice** alla directory **2025**.

5. Sei nella directory **Progetti** (directory principale). Copia script.sh dalla directory **codice** alla directory **mensile**.

6. Sei nella directory **archivio**. Copia script.sh dalla directory **codice** alla directory **febbraio**.

7. Sei nella directory **src**. Copia script.sh dalla directory **codice** alla directory **2024**.

---

## SECONDA PARTE: Path Relativi

Usa **esclusivamente path relativi** per tutti gli esercizi seguenti.

1. Sei nella directory **codice**. Copia script.sh nella directory **documenti**.

2. Sei nella directory **codice**. Copia script.sh nella directory **test**.

3. Sei nella directory **laboratorio**. Copia script.sh dalla directory **codice** alla directory **settimanale**.

4. Sei nella directory **backup**. Copia script.sh dalla directory **codice** alla directory **mensile**.

5. Sei nella directory **gennaio**. Copia script.sh dalla directory **codice** alla directory **src**.

6. Sei nella directory **archivio**. Copia script.sh dalla directory **codice** alla directory **febbraio**.

7. Sei nella directory **2025**. Copia script.sh dalla directory **codice** alla directory **test**.

---

## Note

- **Path assoluto**: parte sempre dalla root (/) o dalla home (~)
  - Esempio: `/home/utente/Progetti/laboratorio/codice`
  
- **Path relativo**: parte dalla directory corrente
  - `../` per salire di un livello
  - `./` per la directory corrente
  - Esempio: `../../backup/settimanale`
    
- Comando per copiare: `cp [origine] [destinazione]`

- Verifica la tua posizione con: `pwd`

- Verifica il contenuto delle directory con: `ls [directory]`

## Consegnare
- File .zip della cartella Progetti finita
- Lista dei comandi usati nella Prima Parte e Seconda Parte
