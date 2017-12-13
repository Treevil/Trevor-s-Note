---
layout: post
title:  "Architettura DBMS: Concorrenza"
date:   2017-12-06 1:18:49 +0100
categories: DataBase
---


Supponiamo che il DBMS riceva contemporaneamente le transazioni T1e T2.
Le transazioni T1e T2 devono godere della proprietà di isolament. 

Dal punto di vista del DBMS, l'esecuzione completa di T1(isolata) seguita dall'esecuzione completa di T2(sempre isolata) ha la proprietà di lasciare la base di dati in una situazione di consistenza.

Se le riceve contemporaneamente, dal punto di vista del DBMS la scelta di eseguire la sequenza T1 T2 oppure T2 T1 è irrilevante.


Se per il sistema informativo è importante l'ordine di esecuzione delle due transazioni, è suo compito mandarle al DBMS nell'ordine corretto.
Se però il sistema informativo manda le due transazioni in parallelo al DBMS, allora il DBMS può eseguirle nell'ordine che vuole.

L'eseguzione in seuquenza delle transazioni è inefficiente. Come sappiamo. Gli accessi alle periferiche sono molto costosi in termini di tempo. Dal punto di vista del DBMS una esecuzione in sequenza lascia tempi morti innaccettabili. Tutti i DBMS sono stati sviluppati in modo da mandare avanti in parallelo operazioni provenienti da transazioni diverse.

Il problema che fare delle operarazionid i interleaving può lasciare la base dati in una situazione d'inconsistenza. Sono stante studiante varie forme di inconsistenza che un interfogliamento può produrre in una base di dati.

Chiamiamo:
- ri (X): Una read della variabile X da parte della transazione Ti
- wj (Y): Una write della variabile X da parte della transazione Tj


**Letture Sporche**
Immaginiamo il seguente interleaving di due transazioni T1 e T2. 

w1(X), r2(X), abort(T1), update2(X), w2(X)

Dopo la write, la transazione T1 viene abortita, ma nel frattempo T2 aveva letto il valore di X modifcato da T1. Il valore letto da T2 è però inconsistente, in quanto prodotto da una transazione T1 abortita. 

**Perdita di aggiornamento**

- T1: r1(X), update1(X), w1(X)
- T2: r2(X), update2(X), w2(X)
dove update1 e uupdate2 sono qualcosa come x = x + 1 

Immaginiamo il seguente interleaving:
 r1(x), r2(X), update2 (X), w2(X), update1 (X), w1 (X)

 DOpo l'esecuzione in sequenza di T1, T2 (o T2 T1), X contettù X + 2. Ma nell'esecuzione parallela si perde l'aggiornamento di T2. 

**Letture non ripetibili**
Situazione: r1(X), w2 (X), r1(X)

Nella seconda read la transazione T1, suppone di leggere il medisimo valore letto durante la prima read, ma nel frattempo, tale valore letto durante la prima read, ma nel frattempo, tale vlore è stato modificato dalla transazione T2, la seconda lettura diventa quindi una lettura non ripetibile.

**Aggionramento Fantasa** 

[Trovare una spegiazione migliore delle slide]

**Interimento Fantasma**

L'inserimento fanstma si verifi sugli insieme

- T1 legge un insieme Xi di dati e calcola la cardinalità (conut(*))
- Durante l'esecuzione di T1, T2, inserisce un elemento in Xi
- T1 ricalcola la cardinalità dell'insieme Xi

La cardinalità letta la seconda volta sarà diversa da quella letta la prima volta, un contrato con la prorietà di isolamento.

<h3>Storia</h3>

La situazione di interlearving delle transazioni si chiamano schedulazione o storia. Una storia è la sequenza di azioni esegute dal DBMS a fronte delle richieste da parte delle transazini.

La gestione della conceorrenza è basata sullì'analisi delle storie possibile che il DBMS può generare.

Semplificazioni:
- Le transazioni leggono e scrivono un oggetto X solo una volta. Si evita quindi il problema delle riletture del medesimo dato escludendo dalla trattazione le letture non ripetibili e gli inserimenti fantasma.

Non si farà cenno alla possibilità che la transazione vada in abort. 

**View-equivalente** La storia S e S' sono equivalenti se sono soddisfatte le seguenti condizioni:
1. S' e S' sono storie definite sullo stesso insieme di azioni (stesse azioni di read e write su stessi dati con gli stessi indici)
2. Condizioni sugli input:
    - Se in S avviene una Ri (X) senza che X sia stato modificato, anche in S' deve avvenire lo stesso.
    - Se in una storia S una Tj scrive l'oggetto X e successivamente Ti legge X, anche nella storia S' deve succedere la stessa cosa.
3. Condzione sullo stato: Se in S una Ti scrive per ultima l'oggetto X, anche S' Ti deve scrivere per ultima l'oggettto X.

La view-equivalenza ci da un criterio rigoroso di confronto tra storie. La transazione è vista come una funzione, ovvero dati gli stessi input, la transazione deve generare gli stessi output. Non è importante la posizione assoluto delle letture e scritte nelle storie, l'importante è che le letture delle transazioni avvangano sui medesimi valori (condizioni sull'input) e lo stato finale della base di datirpodotto da storie equivalenti sia il medesimo (condizione sullo stato del DB)

Applicazione dell'equivalenza

Sappiamo a priori che una storia di transizioni eseguita in successione è per definione corretta perché la transazione gode della proprietà di consistenza, quindi se la transazione è applicata ad uno stato di DB consistente, la transazione lascerà la DB in uno stato consistente.

Se si esegue T1 su uno stato consistente e T1 lascia la DB in uno stato consistente T2 opera su uno stato consiste e lascera il DB in uno stato sostistente (stesso discorso per T2 T1).

Se partiamo da storie corrette (le diverse esecuzioni seriali) e abbiamo una storia di interleaving, possiamo concludere che la storia di interleaving è corretta se è view-equivalenete ad una qualsiasi storia seriale.

Il criterio di serializzabilità dice quindi che una storia S è corretta se è view-equivanete ad una storia seriale qualsiasi delle transazioni coinvolt da S. 

Nota: Date n transazioni esistono n! storie serili.

<h5>Esempio</h5>

Storia(T1T2): r1(A),w1(A),r1(B),w1(B),r2(A),w2(A),r2(B),w2(B)S <br>
Storia    S2: r1(A),w1(A),r2(A),w2(A),r1(B),w1(B),r2(B),w2(B) <br>
- Le due storie condividono il medesimo insieme di azioni
- T1legge A senza che A sia stato modificato prima
- T1legge B senza che B sia stato modificato prima
- T2legge A dopo che T1 lo ha modificato
- T2legge B dopo che T1 lo ha modificato
- T2è l'ultima a scrivere A
- T2è l'ultima a scrivere B

La storia S2 è serializzabile...

<h5>Esempio2 </h5>
Storia(T1T2): r1(A),w1(A),r1(B),w1(B),r2(A),w2(A),r2(B),w2(B) <br>
Storia(T2T1): r2(A),w2(A),r2(B),w2(B),r1(A),w1(A),r1(B),w1(B)
Storia S1: r1(A),r2(A),w2(A),r2(B),w1(A),r1(B),w1(B), w2(B)

- Le due storie condividono il medesimo insieme di azioni
- T2 legge A prima che T1lo abbia modificato
- T1 legge A prima che T2lo abbia modificato

<br>[S1 non è equivalente né alla storia T1T2, né alla storia T2T1]

Mettere a confronto 2 storie ha complessità polinomiale. L'utilizzo dell'equivalenza per verificare il criterio di serializzabilità richiede un numero n! di confronti.

Per poter risolvere il problema ci si è messi in un contesto meno generale della view-equivalenza.

In questo contesto sono importanti le <b>azioni in confitto</b> una storia


In una storia sono in conflitto le seguenti azioni: 
- S1: …ri(X),…,wj(X),… (conflitto)
- S2: …wi(X),…,rj(X),… (conflitto)
- S3: …wi(X),…,wj(X),… (conflitto)
- S4: …ri(X),…,rj(X),… (non c'è conflitto)

Le azioni in conflitto riguardano azioni provenienti da transazioni diverse sullo stesso oggetto...

Sono state chiamate azioni in conflitto perché cambiando l'ordine delle due operazione può cambiare l'attività sulla base di dati o la risposta delle transazioni.

s1:... ri(X),..., wj(X),...
- Se invertiamo Ti legge il prodotto della write di Tj su X
s2: ... wi(X), ..., rj(X),...
- Se invertiamo Tj non legge più il prodotto della write di Ti su X
S3: ...wi(X),..., wj(X),...
- Se invertiamo, si può modificare lo stato finale della base di dati (se wj(X), fosse stata l'ultima write, scambiando l'ordine diventa wi(X) l'ultima write ad essere eseguita)




Grafo dei conflitti 

Data una storia S, il grafo dei conflitti di S è un grado orientato che ha:
- **come nodi** Le transaizoni Ti che compongono la storia
- **come archi** (di conflitto):
    - Considero tutte le letture ri (X) delle transazione sull'oggetto X, si ispeziona la storia da ri(X) in avanti cercando una wj(X): se esiste, si traccia l'arco $$ Ti \rightarrow Tj$$
    - Considero le wi(X) e ispzionando la storia da wi(X) in avanti: ogni volta che si trova una rj(X) lungo il percorso, traccia l'arco $$ Ti \rightarrow Tj $$, fino a qundo non si trova una Wh(X) e si costruisce l'arco $$T_i \rightarrow T_h $$

Nota: Gli archi sono *unici*


Condizione sufficiente, ma non necessaria, di serializzabilità dk unastoria S è che il grado dei conflitti di S sia aciclico.


todo: [Esempio e miglioramenti generali]

Qualsiasi ordinamento toologico del grafo dei conflitti aciclico è una storia seria equivalente alla storia originale.

Quindi per verificare che un interleaving sia equivalente ad una storia seriale qualsiasi construire il grado dei conflitti e verificare che sia aciclico.



<h3>Gestione della concorrenza</h3>
Esistono diversi metodi di gestione della concorrenza, ma si possono tutti dividere in due grosse categorie:

- Metodi ottimistici 
- Metodi pessimistici 

**Metodi ottimistici:** Sono metodi che lanciano le azini delle transazioni a mano a mano che le azini vengono richieste senza particolari controlli. Quando la transazione giunge al commit il DBMS da un controllo per verificare che la storia è serializzabile, se non lo è forza un rollback. Sono detti ottimistici perché partono dall'assunto che le transazioni non generano conflitti nelle storie. Per varie motivazioni, non li tratteremo.

<h4>Metodi pessimistici: Lock</h4>
Partano dall'assunto che ogni transazine può prourre delle storie non serializzabili. I metodi non ottimistici prevengono la non serializzabilità della storia. Presenteremo il metodo basato sui lock perché il più diffuso nei DBMS.


Il DBMS mette a disposizione delle transazioni i seguenti comandi che permettono di chiedere delle autorizzazioni a compurere azioni su ottetti.
- LS(X): Lock shared sull'oggetto X
- LX(X): Lock exclusive sull'ogetto X
- UN(X): unloack sull'oggetto X.

Possiamo assimilare l'oggetto X ad una tupla

**Lock shared**: Quando una transazione Ti vuole eseguire un'azione ri (X) prima di effettuare la terrua deve aver acquisito almeno il lock shared sull'oggetto X, overo il permesso per leggere l'oetto X. Il lock shared (condiviso) si chiama cosi perhé transazioni diverse possono acquisire il lock shared sul medesimo oggetto. Il lock shared può essere quindi concesso dal DBMS a più transazioni. Ad esempio: la transazione Tj può chiedere e ottere il LS sull'oggetto X già ottenuto dalla transazione Ti

**lock Exclsive**: Il LX richiedee un aacesso esclusivo all'oggetto X da parte di una transazione Ti. La richiesta di lock exclusive è di una norma fatta da una transazione per modificare un oggetto X: questa autorizzazione deve sempre precedere una wi(X). Quando Ti ha acquisito l'autorizzazione esclusiva a scrivere l'oggetto X, nessun'latra transazione può acquisire lock sullo stesso oggetto (ne LS ne LX), cioé, la transzione Ti diventa proprietaria esclusiva di X.

Gestione del Lock

Le transazioni possono lanciare attività parallele sui medesimi oggetti. Come viene amministrata dal DBMS la compresenza di più lock?

Il DBMS si avvale della tabella di compatibilità:

| Permesso \ Richiesta | LS      | LX   |
|----------------------|---------|------|
| LS                   | Concede | Nega |
| LX                   | Nega    | Nega |


Ad esempio se Ti posssiede il lock sull'oggetto X e Tj ne fa richiesta, il DBMS concede o nega il lock a seconda dei casi elencati nella tabella di compatibilità.


Gestione del lock
Quando il DBMS non può concere il lock, la transazione richiedente va in **wait** (stato di attesa)

Quando una transazione non ha più bisogno di leggere/scrivere l'oggetto X, può rilasciare il lock (shared o exclusive) attraverso l'unlock.

Per governare queste situazioni, il DBMS mantiene una tabella dei lock.



