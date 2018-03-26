# Meccanica statistica

## Costante di Boltzman
L'unità della misura della temperatura è stata inventata da Lord Kelvin e prende il nome di Kelvin (K), questa unità basa la sua scala in relazione allo zero assoluto. Questa unità di misura è stata creata allo scopo di essere conveniente da manipolare dal lato umano. La temperatura di un oggetto è estremamente legata alla energia che esso possiede. La temperatura di un gas ad esempio corrisponde all'energia cinetica delle molecole. La misura della temperatura è sata stabilita prima che si sapesse che temperatura equivale a dire energia. La costante di Boltzman serve per la conversione delle unità dalla scala umana a quella di energia. L'energia di un gas diluito è `E = 3/2 k_b t_k` dove `k_b` rappresenta la costante di Boltzman e `t_k` la temperatura con unità di misura umane (Kelvin). Da qui si può calcolare la costante che è circa `k_b = 1.4 * 10^-23 [j/k]`, da qui possiamo definire una nuova temperatura `T = k_b * t_k`.

## Entropia
Carnot che era un ingegnere per la costruzione di motori a vapore definì per primo l'entropia  come `s_{carnot} [j * k]` che è collegata all'entropia di Boltzman `S = - sum_i p(i) log(p(i))` dalla costante di Boltzman dove `S = s_{carnot} / k_b`.


## Temperatura
La temperatura è una quantità unità derivata che deriva dalla conoscenza di energia ed entropia.
Prendiamo un sistema aperto che scambia informazioni con l'ambiente che lo circonda, esso ha un insieme di stati che chiameremo `i` con associata una probabilità di essere in quello stato `p(i)` ed un energia `E_i`. Dopo un certo periodo di tempo la probabilità che il sistema si trovi in uno stato dipenderà da `<E>` ovvero `p(i, <E>)` ovvero per ogni `<E>` esiste una famiglia di probabilità di distribuzione `p(i,<E>)`. A questo punto possiamo scrivere l'entropia come funzione dell'energia con `S(<E>) = - sum_i p(i,<E>) log(p(i,<E>))`. Per cambiare l'entropia di un bit (`log 2`) dobbiamo cambiare l'energia media di `\Delta = \partial E / \partial S * \Delta S`. La temperatura viene definita come `T = \partial E / \partial S`.

## Esempio
Prendiamo due sistemi chiusi `A` e `B` con differente temperatura, se li connettiamo l'energia inizierà a fluire dal più caldo al più freddo.
- `S = S_A + S_B`
- `dE_A = - dE_B` (Prima legge della termodinamica)
- `dS_A + dS_B > 0` (Seconda legge della termodinamica)
- `dE_A = T_A * dS_A`
- `dE_B = T_B * dS_B`
