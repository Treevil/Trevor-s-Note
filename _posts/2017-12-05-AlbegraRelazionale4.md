---
layout: post
title:  "Algebra Relazionale: Ottimizzazione"
date:   2017-12-05 8:18:49 +0100
categories: DataBase
---

L'ottimizzazione delle interrogazioni

Come possiamo fare affinché le nostre interrogazioni siano il più veloci possibili?
Vediamo l'ottiizzazione in tempo.

Quando viene richiesta una tupla, il DBMS deve trasferire la pagina dalla periferica di storage alla memoria centrale(buffer). IL DBMS deve trasferire una pagina dalla periferica di storage alla memoria centrare (buffer).

L'ordine di grndezza di questa operazione è di millisecondi. Che confrontato coi tempi di lavoro del processore è milioni di volte più lenta!

Visto che le attività all'interno del DBMS sono minime, i DBMS se voglio minimizzare i tempi di risposta devono minimizzare il trasferimento di pagine.


L'ottimizzazione delle query avviene in due fasi: Ottimizzazione logica e suggessivamente un ottimizzazione fisica.

**Ottimizzazione Logica**: Questa fas è indipendente dalle strutture di memorizzazione. L'ottimizzazione logica prende in input l'albero di parsificazione (albero sintattico) scritto dall'utente e lo trasforma sfruttando le **proprietà dell'algebra relazione** creando un albero equivalente all'originale.


**L'ottimizzazione fisica** Prendere in input l'albero prodotto dall'ottimizzatore logico.
L'ottimizzatore fisico entra nei nodi(operatori) dell'albero di parsificazione, li esamina e in basi alle strtture fisiche sceglie l'algoritmo ottimale per eseguirli.

Alla fine l'albero di parsificazione avrà, come nodi, gli algoritmi più adatti per l'esecuzione ottimale dei nodi.

<h3>Ottimizzatore Logico</h3>

L'uristica di questo componente è semplice: ridurre la massa di tuple concettualmente coinvolte dall'interrogazine.

Quasi tutte le operazioni principali dei sistemi informativi che usiamo quotidianamente sono mirate a lavorare su pochissimi dati: lavoro sul mio piano di studi, non tutti. Lavoro sui miei pazienti, non tutti, Opero sul mio conto in banca, non tutti i conti correnti (anche se ci potrebbe piacere, ehehehe...). 

Entra quindi in gioco la selezine, per limitare fin da subito il numero di tuple e spingere l'operazione più in basso possibile all'interno dell'albero.

<h4>Algoritmo di ottimizzazione logica</h4>

1. Decomposizione degli AND
2. Trasferire le selezioni verso le foglie finché è possibile con le proprietà distributive della selezione. 
3. Trasferire le proiezioni verso le foglie finché è possibile con le proprietà distributive delle proiezioni.
4. Ricondurre ad un unica selezione le selezioni multiple
5. Riconoscere le sequenze di join
6. Riconoscere le sequenze di Join
6. Ricondurre ad un unica proiezione le proiezioni mmultiple
7. Esame delle varianti dell'albero di parsificazione dovute alle proprietà associative (scegliere la variante di costo minimo)


Segue spiegazione algoritmo.



