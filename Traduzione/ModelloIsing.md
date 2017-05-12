# Modello Ising (wiki)
Il modello di Ising (Ernst Ising) è un modello fisico matematico studiato in meccanica statistica. Inizialmente ideato per descrivere un corpo magnetizzato è stato poi utilizzato per fenomeni variegati accumunati dalla presenza di singoli componenti che interagiscono a coppie.

## Definizione
Il modello è definito su un insieme discrieto di variabili, libere di assumere valori `+1` o `-1` che costituiscono i nodi del reticolo. Possiamo immaginare un nodo come un atomo il cui momento magnetico elementare o "spin" può allinearsi lungo due direzioni su (`+1`) o giù (`-1`). I nodi `S_i` interagioscono a coppie: l'energia ha un valore quando i due nodi di una coppia sono uguali e un altro quando sono diversi.

## Modellizazione
L'energia è definita come:
`E = - sum(J_ij * S_i * S_j; i, j) + B * sum( S_i; i)`
dove la somma conta ogni coppia solo una volta.
Notiamo  che il prodotto dei nodi è `+1` se sono allineati e `-1` se sono anti-allineati. Il parametro `J` risulta metà della differenza in energia trai i due casi. L'interazione magnetica tende ad allineare tutti gli atomi in una certa direazione mentre il rumore termico tende a perturbare l'ordine. Il vettore di spin è in generale un vettore tridimensionale e se viene trattato come tale nel modello di Ising, questo è detto Sferico. In talune situazioni può però accadere, per la precisa conformazione del reticolo cristallino del materiale che tutti i vettori diano orientati in un medesimo piano in modo da poter definire un modello di Ising planare. Se invece tutti i vettori sono orientati in una particolare direzione in tal caso di arriva a definire il modello di Ising monodimensionale.