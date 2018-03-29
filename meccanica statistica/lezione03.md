# Meccanica statistica

## Ripasso
- `S = - \sum_i p(i) log(p(i))`
- `\sum_i p(i) = 1`
- `\sum_i p(i) E(i) = <E>`
Dato un sistema con una distribuzione di probabilità e non in equilibrio, la distribuzione di probabilità tende sempre ad allargarsi man mano che il sistema si avvicina all'equilibrio.


## Ground state
Lo stato fondamentale di un sistema è una distribuzione di probabilità in modo che valga `0` ovunque tranne nello stato di energia inferiore.

# Prima legge della termodinamica
`dE / dt = 0`

# Seconda legge della termodinamica
`dS > 0`

# Legge zero della termodinamica
Prendiamo un sistema composto da due parti separate `A`, `B`, che vengono connesse in modo che la temperatura possa fluire. La temperatura continuerà a fluire dall'oggetto più caldo a quello meno caldo fino a quandola differenza di temperatura tra i due non si annulla e raggiungono così un equilibrio termico.
Supponiamo ora che `T_B > T_A` con `T_B, T_A > 0`. Scrivendo le leggi che conosciamo:
- `dE_A = - dE_B` (Prima legge della termodinamica)
- `dS_A + dS_B > 0` (Seconda legge della termodinamica)
- `dE_A = T_A * dS_A`
- `dE_B = T_B * dS_B`
Possiamo riscrivere:
- `dE_A + dE_B = 0 = T_A * dS_A + T_B * dS_B`
Isolando `dS_B`:
- ` dS_B = - T_A / T_B * dS_A`
Sostituendo nella seconda legge possiamo scrivere:
- `dS_A (1 - T_A / T_B) > 0`
- `dS_A (T_B - T_A) > 0`
Sapendo che `T_B - T_A` è un numero positivo per ipotesi, concludiamo che `dS_A > 0`.
Moltiplicando per `T_A` otteniamo `dE_A = T_A * dS_A > 0` e quindi `dE_B < 0`, in altre parole l'energia si sposta da `B` ad `A`.

## Approsimazione di Stirling
`N! = N^N * e^-N`
Prova:
- `log(N!) = \sum_{x=1}^N log(x)`
- `log(N!) = \integrate_1^N log(x) dx`
- `log(N!) = [x log(x) - x]_1^N`
- `log(N!) = [N log(N) - N] - [1 log(1) - 1]`
- `log(N!) = log(N^N) - (N - 1) ~= log(N^N) - N`
- `N! = N^N e^-N`

## Sistema non chiuso
Pensiamo un sottosistema `A` contenuto in un sistema molto più grosso `B` che fa da bagno termico.
Se il sistema `B` è moltro grosso anche se un po' di energia viene trasferita ina `A` la temperatura non di `B` non cambia. Una scelta che risulta spesso comoda di `B` è considerarlo come una catena di `N` elementi della stessa dimensione di `A`, dove `N` è un numero molto grande.
Il numero di occupazione `n_i` è il numero di sistemi che sono nello stato `i`.
Costrizioni:
- `n_1 + ... + n_N = N`
- `n_1 * E_1 + ... + n_N * E_N = E_{tot} = N * <E>`
- `p(i) = n_i / N`
Supponiamo ora che `N` sia un numero finito e che `E` possa assumere un numero infinito di valori.
La maggior parte degli `n_i` saranno `0`. Il numero di collezioni di stati che possiamo avere sono `N! / (n_1! * ... * n_N!)`. Cerchiamo di massimizzare `log()`.

(1:09:30)
