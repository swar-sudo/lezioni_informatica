# Percorsi assoluti e relativi

## Storia dei nomi di file

Nel vecchio sistema operativo DOS, il nome di file aveva una struttura fissa di 8 caratteri, un punto, e altri 3 caratteri (detti estensione). L'estensione serviva a identificare il tipo di file: `.jpg` per file immagini JPEG, `.txt` per file di testo puri, `.doc` per file Word, etc.

Su Linux (e per buona parte anche in Windows), un nome di file è una stringa di caratteri qualunque, e può contenere quanti punti si desidera (anche nessuno). L'estensione non è necessaria, ma la si aggiunge per facilitare l'utilizzatore, che è in grado di riconoscere il tipo di ogni file.

In Linux, l'estensione del file può essere anche più lunga di 3 caratteri: ad esempio `.html` è l'estensione standard per i file HTML.

## Pathname

All'interno del file system possono esserci molti file con lo stesso nome, ma che si trovano in directory diverse, pertanto per indicare con esattezza uno specifico file, in modo da non far sorgere ambiguità, vengono utilizzati i **pathname** (nomi dei percorsi) che possono essere di due tipi: assoluti o relativi.

## Percorsi assoluti

Un percorso assoluto è una stringa del tipo:

```
/<nomedir>/<nomedir>/<nomedir>/<nomefile>
```

Inizia con la barra di divisione, ha una serie di componenti separati da barre e termina con un nome di file. La sequenza dei vari `<nomedir>` è la sequenza di directory dentro le quali il sistema deve entrare, partendo dalla radice, per raggiungere la directory dove si trova il `<nomefile>` desiderato.

### Esempi

- `/home/giovanni/file.txt` si riferisce a `file.txt` (nella home directory di giovanni).
- `/abcd` si riferisce a un file di nome `abcd` (senza estensione) dentro la directory radice.

### Punti importanti

- Il percorso assoluto deve iniziare con la barra di divisione.
- La barra da utilizzare è quella per la divisione (`/`) e non la barra retroversa (`\`) che si usa invece nei sistemi Windows.
- È necessario specificare la sequenza completa di tutte le directory da attraversare per arrivare al file desiderato.

## Directory corrente

Quando si specifica un nome di file direttamente, senza percorso, il file viene cercato e quindi eseguito in questa directory.

Per cambiare directory corrente nella shell di Linux, si può usare il comando `cd` (change dir).

Più in generale, la directory corrente serve come punto di riferimento per i percorsi relativi.

## Percorsi relativi

Un percorso relativo è una stringa di questo tipo:

```
<nomedir>/<nomedir>/<nomedir>/<nomefile>
```

Quindi è simile a un percorso assoluto ma non ha la barra iniziale. Anche il significato è simile a quello di un percorso assoluto, con la differenza che la directory da cui iniziare la ricerca del file non è la directory radice ma la directory corrente.

Nei percorsi relativi si usa spesso una directory speciale, la directory `..` (due punti), detta anche directory padre o directory precedente (di quella corrente), che consente di risalire l'albero delle directory.

### Esempi

Se la directory corrente è `/home`, allora:

- `giovanni/file.txt` si riferisce a un file `file.txt` nella home directory di giovanni.
- `../abcd` si riferisce a un file di nome `abcd` (senza estensione) dentro la directory radice.
