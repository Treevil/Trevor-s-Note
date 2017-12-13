---
layout: post
title:  "Ottimizzatore dei DBMS"
date:   2017-12-06 1:18:49 +0100
categories: DataBase
---

Come già definito in precedenza, l'ottimizzatore ha due fasi:
- Ottimizzatore logico, che lavora sull'albero di parsificazione
- Ottimizzatore fisico, considera l'albero prodotto dall'ottimizzazione logica e sceglie gli algoritmi da abbinare ai nodi operativi.

Esistono più algoritmi per ogni tipo di nodo operativo

<h3>Ottimizzazione delle selezioni</h3>
Per semplicità trascureremo la presenza di OR nel predicato di selezione.

Consideriamo la seguente selezione

$$\sigma_{\psi \wedge p_1 \wedge p_2 \wedge ... \wedge p_h }$$

- $$ \psi $$: Componente non risolubile (non esiste nessun indice che aiuta a risolvere il predicato)
- $$p_1 .. p_h$$: Predicati risolubili (su attributi con indice)


Esempio:
STUDENTI (<u>MATR*</u>, Nome*, DataNascita*, Genere, Indirizzo)

$$\sigma_{Nome="Piero" \wedge DataNascita > '1990' \wedge Indirizzo='TO' } $$

(*) Attributi con indice 



La prima strategia di ottimizzazione consiste nel'usare ogni indice disponibile, ovvere sfruttano gli indici per ottenere gli insiemi di RID

$$\{RID\}_p1, \{RID\}_p2, ..., \{RID\}_ph$$

Successivamente calcolano l'intersezione degli insiemi di RID:

$$ R_p = \{RID\}_p1 \cap \{RID\}_p2 \cap ... \cap \{RID\}_ph $$

L'insieme R_p di RID viene portato in memoria centrale e filtrato in base al predicato $$\psi $$

Il costo della prima strategia è dato dal costo di accesso agli indici, mentre il costo di acesso al predicato $$ \psi$$ viene ignorato, in quanto applicato su record già presenti in memoria centrale.

I DBMS invece usano una strategia diversa:
- Considerano l'ipotesi di scansione sequenziale che costra $$N_page (T) $$
- Degli indici a disposizione scelgono quello che conviene di più, trascurando gli altri.
- Caocloano quindi i costi di accesso $$ C_p1, C_p2, .., C_ph$$
- L'ottimizzatore sceglie la tecnica di accesso con l'indici più selettivo
- Tutte le condizioni vengono verificate in memoria centrale

Alcuni benchmark mostrano che i DBMS che usano solo un indice hanno un'efficienza confrontabile con quella dei DBMS che usano tutti gli indici. Questi ultimi hanno degli overhead maggiori dovuti all'elaborazione delle lista di RID.
In ogni caso se il costo dell'accesso sequenziale è minore del costo con indici, gli indici non vengono usati da nessuna delle due strategie.
Se un indicie non viene mai usato da n DBMS, ci sono solo costi di mantenimento senza benefici. 

<h3>Gli algoritmi di join</h3>
 L'operatore di join è il più critico in tutti i DBMS, perché comporta confronti tra tuple di due tavole.

Esistono diversi classi di algoritmi di Join. Ma prendiamo in cosiderazione il caso generico di theta hoin tra due tavole R ed S: $$R \Join_\sigma S $$


La prima tecnica (Nested Loop) la più semplice che si possa immaginare e consiste nella comparazione delle tuple di R con le tuple di S.

Nell'architettura delle basi di dati, possiamo immaginare la tecnica di implementazione in questo modo: Due loop, un loop esterno sulle pagine di R, un loop interno è sulle pagine di S  che vengono quindi lette tutte più volte (una per ogni pagina di R). Il join tra $$R_i$$ ed $$S_h$$ viene eseguito in memoria centrale, quindi ha un costo irrelevante.

Sul piano dei costi, il DBMS trasferisce in tutto:

Costo = $$ N_{page} (R) + N_{page} (R) * N_{page} (S)

Sembra molto costoso, ma si può usare un accorgimento per ridurre in modo sensibile il costo. 

<h4>Nested Block Loop</h4>

Nel buffer abbiamo B pagine. Usiamo B - 1 pagine per caricare le pagine di R e la B-esima pagina scorre le pagine di S. Fino a quando ho esaurito tutta la tavola S. Poi carico le restanti pagine di R. 

Anziché caricare una pagina di R e poi eseguire il loop intermo, si caricano blocchi di B - 1 pagine di R, e per ogni blocco eseguo un loop completo su S.

Il costo di questa implementazione è quindi:

$$ Costo =  N_{page} (R) + (N_{page} (R)/(B-1)) * N_{page} (S) $$

Considerando che i buffer reali sono molto capienti il costo viene ridotto di parecchio.

Visto che il Join è commutativo (Fare A Join B è uguale a fare B Join A), il DBMS può scegliere la relazione con meno pagine come relazione esterna.

<h4>Nested Loop con indice</h4>

Consideriamo il caso generico del theta Join tra due tavole R ed S: 

$$  R(...A..) \Join_{\sigma(A,B*)} S(...B...) $$

con l'ipotesi che sull'attributo B esista un indice. <br>

Il discorso può essere esteso al caso di condizione su più attributi.

Immaginiamo un indice di tipo B+Albero su B

L'algoritmo del nested loop con indice è il seguente:


1. Carica una pagina di S
    1. Per ogni pagina prendi una tupla 
        1. Prendi il valore della tupla in corrispondenza di A (t[A]) 
        2. Effettua una interrogazione su S che può sfruttare l'indice
        3. Restituisce le tuple che soddisfano le condizone e vengono utile con tutte quelle che hanno soddisfatto l'interrogazione del punto precedente

Cardinalità: Vedere....


Altri algoritmi di join:
- Hash-Join: Algoritmi basati sulle funzioni di hash e utilizzati solo negli equi-join
- Sort-merge join: Algoritmi basati sull'ordinamento e la fusizione dei risultati parziali.

L'ottimizzatore fisico considera ovviamente anche altri operatori:
- Unione e differenza insiemistica
- Proienzioni
- Richieste di ordinamento
- Presenza del distinct

