
# Guida CMD Challenge
- Accedi a https://cmdchallenge.com/
- Crea un documento da consegnare che salvi tutti gli step del gioco che sei riuscito a completare


---

## 1. Navigazione e gestione file

- `pwd` – mostra la directory corrente  
- `ls`, `ls -l`, `ls -a`, `ls -R` – elenca file e directory  
- `cd <cartella>` – cambia directory  
- `mkdir`, `mkdir -p` – crea directory (anche annidate)  
- `rm`, `rm -r`, `rm -rf` – rimuove file e directory  
- `cp`, `cp -r` – copia file o cartelle  
- `mv` – sposta o rinomina file  
- `touch` – crea file vuoto o aggiorna timestamp  
- `ln -s` – crea collegamenti simbolici  

---

## 2. Visualizzazione e manipolazione testo

- `cat` – visualizza contenuto file  
- `head`, `tail` – mostra le prime/ultime righe di un file  
- `grep` – cerca testo o pattern (opzioni: `-r`, `-i`, `-h`, `-c`, `-l`, `-o`)  
- `sort` – ordina righe di un file  
- `wc` – conta righe, parole, caratteri (`-l`, `-w`, `-c`)  
- `tr` – sostituisce o elimina caratteri  
- `sed` – sostituisce testo all’interno di file  
- `awk` – analizza e trasforma testo su base di colonne  

---

## 3. Ricerca e operazioni ricorsive

- `find . -type f` – elenca file ricorsivamente  
- `find . -name '*.txt'` – cerca per nome o estensione  
- `grep -r` – ricerca ricorsiva di testo nei file  
- `rm -r`, `cp -r` – applicano operazioni ricorsive  

---

## 4. Combinazioni e redirezioni

- Uso delle pipe (`|`) per collegare comandi  
- Redirezione: `>` (sovrascrive), `>>` (aggiunge), `<` (input da file)  
- Esecuzione condizionale: `&&` (se vero), `||` (se falso), `;` (in sequenza)  
- Sostituzione di comandi: `$(comando)`  

---

## 5. Pattern, espressioni regolari e globbing

- Caratteri jolly: `*` (qualsiasi), `?` (un singolo carattere)  
- Espansione con parentesi graffe: `{1..10}`, `{a,b,c}`  
- Regex: `^` inizio, `$` fine, `.` qualsiasi carattere, `[]` insiemi, `+`, `*`, `?`, `|` alternative  
- File nascosti: iniziano con `.` e si visualizzano con `ls -a`  

---

## 6. Strumenti per contare e calcolare

- `wc -l`, `wc -w`, `wc -c` – conteggi vari  
- `xargs` – costruisce comandi da input  
- `bc` – calcolatrice da terminale  
- `seq 1 10` – genera sequenze numeriche  

---

## 7. Permessi e proprietà

- `ls -l` – mostra permessi e proprietari  
- `chmod` – modifica permessi (numerici o simbolici)  
- `chown`, `chgrp` – cambia proprietario o gruppo  

---

## 8. Buone pratiche e consigli

- Eseguire sempre `ls` prima di `rm` per verificare il contenuto  
- Usare virgolette per gestire nomi con spazi  
- Provare comandi in directory di test  
- Consultare `man <comando>` per ulteriori dettagli  
- Usare opzioni interattive (`-i`) quando disponibili per confermare azioni  

---

Questa guida raccoglie i comandi e i concetti più utili per affrontare le sfide del **CMD Challenge**.  
È pensata come riferimento rapido per lo studio e la pratica dei comandi Unix/Linux.
