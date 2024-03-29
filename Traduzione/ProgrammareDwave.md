# Programmare D-Wave

## Introduzione
Il computer quantistico utilizza i qubit per memorizzare l'informazione. I qubit sono governati dalle leggi della meccanica quantistica e permettono l'utilizzo delle superposition. Una superposizion è una sovrapposizione coerente degli stati 1 e 0 che dopo un evento esterno collassa in uno dei due stati. Questa proprietà regala al computer quantistico l'abilità di risolvere velocemente una certa classe di problemi complessi di ottimizzazione, machine learning e campionamento.
Programmare un computer quantistico è molto differente dal programmare un computer tradizionale. Per programmare il sistema quantistico bisogna mappare il problema in una ricerca del puto minimo in uno scenario il quale rappresenta la solizione migliore a tale problema. Il processore considera simultaneamente tutte le possibili soluzioni per determinare quella con l'energia di sistema minore. Essendo il quantum computer un sistema probabilistico invece che deterministico ritorna un un numero elevato di risposte in breve periodi di tempo, 10000 al secondo. In qusto modo ristorna le informazioni non solo della soluzione ottimale ma anche delle valide alternative. Successivamente analizzeremo come trasformare il problema di colorare una mappa in un programma da dare in pasto al computer quantistico.

## Problema
La mappa del Canada è composta da dieci provincie e tre territori. Tipicamente viene assegnato un colore a ciascuna delle tredici regioni in maniera tale che le regioni adiacenti non presentino lo stesso colore. Le ragioni isolate come ad esempio le isole non fanno parte delle adiacenze. L'idea di che due regioni con lo stesso colore dividano uno stesso bordo è pensato per rendere più evidenti i confini delle regioni. Da qui è naturale porsi il seguente problema: quanti colori sono necessari per colorare la mappa? e sopratutto, quant'è il numero minimo di colori?

## Modello di programmazione
L'unità base per il calcolo sono i qubit. I qubit sono delle semplici variabili che possono essere impotate a 0 o a 1. Quando programmiamo non impostiamo direttamente i qubit ma gli influenziamo in due modi: primo associamo ad ogni qubit `\q_i` ad un peso `\a_i`; secondo associamo ad ciascuna coppia di qubit `\q_i \q_j` una forza `\b_ij`. Ora che abbiamo introdotto i concetti di peso e di forza possiamo definire la funzione di oggetto.
`\O(a, b; q) = SUM(\a_i \q_i; i=1; N) + SUM (\b_ij q_i \q_j; i,j)`
Questo funzione definirà la distribuzione da cui saranno selezionati i nostri campioni. La prima sommatoria rappresenta i pesi dei qubit, la seconda rappresenta la forza tra le coppie. La cosa importante da osservare è ogni istruzione di macchina quantistica consisterà nel impostare i valori di `a` e `b`.

## Colorazione di una regione
Scegliamo `C` come numero di colori. Per ogni reglione associamo `C` qubit, uno per colore. Siccome ogni regione può avere un solo colore selezionato contemporaneamente se il qubit indicante il colore rosso (per esempio) sara acceso, vorrà dire che gli altri `C-1` saranno spenti.
Per semplicità iniziamo dal risolvere il problema con due colori. La nostra funzione oggetto sarà:
`\O(a, b; q) = \a_1 \q_1 + \a_2 \q_2 + \b_12 \q_1 \q_2`
Enumeriamo i quattro possibili stasi della nostra distribuzione.
| \q_1 | \q_2 | \O(a, b; q) |
|---------------------------|
| 0 | 0 | 0 |
| 0 | 1 | \a_2 |
| 1 | 0 | \a_1 |
| 1 | 1 | \a_1 + \a_2 + \b_12 |
Dobbiamo fare in modo che gli stati `(0,1,q)` e `(1,0,q)` siano i favoriti rispetto gli altri. Per far ciò dobbiamo attribuirli un "energia" inferiore assegnandoli un valore basso come ad esempio `\a_1 = \a_2 = -1`. Lo stato `(1,1,q)` è proibito qundi gli assegnamo un valore alto attraverso il parametro `\b_12 = 2`.
Per passare al caso con `C = 3` bisogna risolvere la tabella di prima considerando la funzione `\O(a, b; q) = \a_1 \q_1 + \a_2 \q_2 + \a_3 \q_3 + \b_12 \q_1 \q_2 + \b_13 \q_1 \q_3 + \b_23 \q_2 \q_3` al posto di quella di `C = 2`. Una considerazione che facilita molto la procedura e legata alla simmetria dei colori, dato che non abbiamo preferenze che una regione sia rossa pittosto che blu allora tutti i coefficenti `\a` e `\b` saranno indistinamente uguali e quindi si potrà scrivere: 
`\O(a, b; q) = \a (\q_1 + \q_2 + \q_3) + \b (\q_1 \q_2 + \q_1 \q_3 + \q_2 \q_3)`. Del tutto analoga la procedura per risolvere il caso `C = 4`.

## Dal qubit logico a quello fisico
Dopo al primo passaggio siamo arrivari a definire una regione, per il caso `C = 4`, come un insieme di 4 qubit con 4 pesi e 16 accoppiamenti di forza. Sfortunatamente al livello fisico la macchina ha dei limiti di collegamentro tra i qubit quindi per risolvere il problema scegliamo di associare una catena di qubit fisici ad uno logico. Per questo problema bisognerà associare due qubit fisici ad uno logico. Nel far ciò bisognerà collegare i 2 fisici con un accoppiamento di forza che cerchi di tenerli allineati e bisognerà ridistribuire i pesi e le forze. Il peso di un qubit fisico in questo caso corrisponderà a per il caso `1/2` logico e così anche ogni suo accoppiamento di forza.

## Collegamento con altre regioni
A questo punto abbiamo codificato i nostri colori nei nostri qubit fisici, il prossimo passo e mettere in comunicazione le regioni adiacenti due a due. Quello che ci interessa in particolare è collegare lo setesso colore in due regioni diverse adiacenti, in modo tale da poter impostare un valore di forza di collegameto elevato per impedire che entrambi siano attivi contemporaneamente. Considerando la tabella di prima come esempio di collegamento tra due regioni possiamo dedurre che vogliamo tenere i parametri corrispondenti agli stati  gli stati `(0,1,q)` e `(1,0,q)` neutri, mentre, lo stato `(1,1,q)` lo vogliamo proibire. Per far ciò impostiamo i parametri come `\a_1 = \a_2 = 0` e `\b_12 = 1`.

## Limite fisico di vicinanza
Il collegamento tra le regioni rappresenta anche esso un problema di collegamento fisico come per i qubit. Per risolvere qusto problema applichiamo una procedura analoga, ovvero, cloniamo le regioni in modo da poter realizzare i collegamenti fisici tra di esse. Si può vedere questo limite rappresentato nella tabella sottostante per le regioni AB, NT, BC.
|   |  0 |  1 |  2 |  3 |  4 |
|----------------------------|
| 0 | NL | ON | MB | SK | AB |
| 1 | PE | QC | NU | NT | AB |
| 2 |    | NB | NS | NT | BC |
| 3 |    |    |    | YT | BC |
Anche in questo caso per ogni regione radoppiata i pesi e le forze andranno aggiustati di conseguenza.

## Conclusioni
Da questo esempio possiamo ottenere tre conclusioni. La prima e che è possibile automatizzare il passaggio da logico a fisico con delle routin e quindi poter semplificare il lavoro del programmatore. La seconda è che la grandezza della mappa che possiamo gestire dipende dal nostro numero di qubit fisici. Ci sono procedure più avanzate che permettono di scomporre mappe più grandi e di gestire i calcoli su pezzi di mappa. La terza e che abbiamo fatto l'esempio con 4 colori ma più generalmente si vuole eseguire problemi più generici che richiederanno più colori e quindi più qubit.

# Implementazione in C
```
/* STEP 1: accendere i qubit */
/* Gestione dei pesi */
for ( i = 0; i < C; i++ ) {
  weight[DW_QUBIT(row, col, 'L', i)] += -0.5;
  weight[DW_QUBIT(row, col, 'R', i)] += -0.5;
}

/* Gestione delle coppi di forza */
for ( i = 0; i < C; i++ )
  for ( j = 0; j < C; j++ )
    if ( i != j ) {
      strength[DW_INTRACELL_COUPLER(row, col, i, j)] += 1;
    }

/* STEP 2: creazione delle catene */
for ( i = 0; i < C; i++ ) {
  weight[DW_QUBIT(row, col, 'L', i)] += 1;
  weight[DW_QUBIT(row, col, 'R', i)] += 1;
  strength[DW_INTRACELL_COUPLER(row, col, i, i)] += -2;
}

/* STEP 3: gestione dei vicini */
/* vicini orizzontali */
if ( col < (DW_N - 1) && is_neighbor(cell_region[row][col], cell_region[row][col+1]) )
  for ( i = 0; i < C; i++ ) {
    strength[DW_INTRACELL_COUPLER(row, col, 'H', i)] += 1;
  }
/* vicini verticali */
if ( col < (DW_N - 1) && is_neighbor(cell_region[row][col], cell_region[row+1][col]) )
  for ( i = 0; i < C; i++ ) {
    strength[DW_INTRACELL_COUPLER(row, col, 'V', i)] += 1;
  }

/* STEP 4: creazione dei cloni */
/* cloni orizzontali */
if ( col < (DW_N - 1) && cell_region[row][col] == cell_region[row][col+1] )
  for ( i = 0; i < C; i++ ) {
    weight[DW_QUBIT(row, col, 'R', i)] += 1;
    weight[DW_QUBIT(row, col+1, 'R', i)] += 1;
    strength[DW_INTRACELL_COUPLER(row, col, 'H', i)] += -2;
  }
/* cloni verticali */
if ( col < (DW_N - 1) && cell_region[row][col] == cell_region[row+1][col] )
  for ( i = 0; i < C; i++ ) {
    weight[DW_QUBIT(row, col, 'L', i)] += 1;
    weight[DW_QUBIT(row+1, col, 'L', i)] += 1;
    strength[DW_INTRACELL_COUPLER(row, col, 'V', i)] += 1;
  }
```