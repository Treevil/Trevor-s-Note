---
layout: post
title:  "Architettura DBMS: "
date:   2017-12-06 1:18:49 +0100
categories: DataBase
---

![Architettura DBMS]({{ "/asset/img/database/architetturaDBMS.png" | absolute_url }}){:class="img-responsive"}

**Gestore delle tanszioni**: Riceve le transazioni e ne gestisce il ciclo di vita inviando i comandi DML alle componenti sottostanti che devono eseguire l'azione richiesta. 

**Serializzatore** è responsabile della proprietà di isolamento

**Gestore del ripristino** Oltre a gestire il ripristino in seguito a gusti è responsabile della proprietà di atomicità. Inoltre deve garantire l'integrità dei dati (se i dati vengono corrotti, il gestore del ripristino cerca di recuperare il dato corretto oppure forza un abort della transazione)

**Gestore del buffer** Responsabile della durabilità

**Consistenza** è di competenza sia del gestore delle transazioni (verifica di tutti i vincoli della base di dati) che del serializzatore.

Consideriamo l'area di lavoro, ovvero la memoria centrale. Nell'area di lavoro abbiamo la transazione $$T_i$$ che richiede la lettura /modifica di un record. La transazione quando richiede l'attività su un record invia delle richieste al gestore del buffer.

La transazione $$T_i$$ invia una richiesta chiamata fix pid che significa: la transazione ha bisogno di avere a disponsizione una pagina dati di indirizzo pid (page identification)


<h3>Le pagine</h3>
Tutti i dati nel database (tablelle, indici, log, dump) sono organizzati in pagine. Le pagine hanno dimensioni che dipendono dal sistema (anche variabili). Queste pagine contengono i record. Se la transazione ha bisogno di lavorare su un ben determinato record (tupla), bisogna cercare una pagina con un certo indirizzo *pid* che si presume contenga il record desiderato.


Le transazione per lavorare su un dato ha sempre bisogno di chiedere al buffer la disponibilità di una ben precisa pagina. Il **gestore del buffer** caricherà la pagina nel buffer stesso, prendendola dalla periferica di storage se non già presente nel buffer.

Il gestore del buffer prende i dati memorizzati nel disco e li mette nella cache presente nella periferica stessa. Dalla cache vengono poste nel buffer della memoria centrale.

Il gestore del buffer risponde alla transazione inviandogli l'indirizzo della memoria centrale in cui si trova la pagina.

La transizione acquisisce, tramite il comando fix pid, il puntatore alla zona di memoria (buffer) che contiene la pagina.

Il caso di lettura, si limita a leggere i dati. 

In caso di update / scrittura, avviene il processo inverso. E' la transizione che modifica i dati nel buffer. Succesivamente il gestore del buffer si occuperò di copiare la pagina con le modifiche nella periferica...

<span class="note">In questo corso la dimensione del blocco sarà uguale alla dimensione della pagina, per semplificare un po' le cose. Normalmente la pagina è composta da un certo numero di blocchi fisici che a loro volta sono composti da un certo numero di settori.</span>

![Architettura Pagina]({{ "/asset/img/database/pagina.png" | absolute_url }}){:class="img-responsive"}

<h3>RID (Record Identification)</h3>

L'archiettura di RID con indice ed offset consente al gestore delle pagine (il file system) la possibilità di modificare la posizione dei record a piacimento all'interno dell'area dati senza influenzare gli indirizzi esterni.

Il gestore deve semplicemente modificare l'offset dell'array rendendo le applicazioni indipendenti dall'array rendendo le applicazioni indipedenenti rispetto alla movimentazione dei record all'interno dell'area dati della pagina.

Immaginiamo di avere una pagina piuttosto piena e che un'applicazione faccia un aggiornamento del record variandone la dimensione (esempio: strnga di caratteri da 100 a 1000). Può succedere che il record non entri più nell'area dati e dev'essere posizionato da un altra parte. La tecnica dell'offset permette l'indirizzamento indiretto.


<h3>Comandi</h3>
- **FIX** Richiesta di accesso ad una pagina
- **USE** Richiesta di untilizzo di una pagina per cui l'applicazione ha già ottenuto accesso
- **UNFIX** quando un'applicazione non ha più bisogno di una pagina e lo cominuca al gestore (CP= CP-1)
- **FORCE** l'applicazione impone al gestore del buffer di trasferire la pagina dal buffer alla periferica
- **Flush** Comando usato dal gestore del buffer per trasferire la pagina.

<h4>Algoritmo di FIX(PID)</h4>
![Architettura Pagina]({{ "/asset/img/database/algoFIX.png" | absolute_url }}){:class="img-responsive"}

In questo algormitmo le periferiche non sono mai toccare direttamente dalle applicazioni, ma ogni modifica viene eseguita soltato su pagine della memoria gentrale. 

La durabilità è compito del buffer (FLUSH).

<h3>Organizzazione dei dati</h3>
Semplicando, possiamo immaginare una pagian come un elenco di record (eventualmente anche parzialmente libera). Una tabella (es: STUDENTI) è organizzata come un elemento di pagine a loro volta contenenti record non ordinati. Esiste tutavia la possiblità di introdurre un ordinamento dei record ( e conseguentemente delle pagine)

Possiamo ad esempio immagine una tabella tudenti ordinata per matricola crescente. se devo inserire ad esempio un record con matricola 700 devo rispettare l'ordinamento. Se c'è spazio nella pagina posso inserirlo ed eventualmente riorganizzo gli offset.

Ma cosa succede se devo inserire un record in una pagina già piena? Posso utilizzare la pagine trabocco (overflow)

Queste pagine determinano un degrado delle prestazioni perché richiede l'acesso ad un altra pagina. Inoltre l'accesso sequenziale, utilizzando il pipelining, viene interrotto per poter accedere a pagine non consecutive della memoria. E' compito del DBA riorganizzare le pagine per eliminare gli overflow eccessivi.

In generale, una pagina fa riferimento ad una ben determinata tabella, i DBMS hanno però la possibilità di **clusterizzare**. 

Consideriamo una tabella <br>
    STUDENTI (<u>MATR</u>, NomeS, Indirizzo)

ed un'altra tabella <br>
    ESAMI (<u>MATR, Corso</u>, Voto, DataE)

i DBMS danno la possibilità di avere pagine / file che mettono innsieme tabelle diverse.

Vengono memorizzati fisicamente adiacenti i record di STUDENTI e ESAMI che si riferiscono alla stessa chiave MATR, velocizzanodo i join.

![Architettura DBMS]({{ "/asset/img/database/esempioCluster.png" | absolute_url }}){:class="img-responsive"}


<h3>Metodi D'accesso</h3>
Esistono 3 grandi categorie di meotidi di accesso 
- Metodo di acesso sequenziale (anche detto seriale)
- Metodo d'accesso tabellare
- Metodo d'acesso diretto


<h4>Sequenziale</h4>

In lettura, l'accesso **sequenziale** implica l'ordinamento su un attributo, ad esempio, nella tavola STUDENTE, posso decidere di ordinare sulla matricola o sul nome e le tuple vengono caricate nelle pagine seguendo l'ordinamento.

In lettura, l'accesso seriale implica l'assenza di ordinamenti e le tuple sono caricane nelle pagine ocosi come arrivano nel file system.

In questo caso durante la selezione del tipo $$\sigma_{x="qualcosa"}(TABELLA)$$ (dove x è chiave)

Cosnideriamo un'organizzaizone dei dati secondo un accesso seriale. Avremmo un'organizzazione a pagine da Pagina 1 a pagina N. Il DBMS, non pò far altro che leggere le pagine una dopo l'altra.

Il DBMS deve calcolare il costo **a priori** dell'accesso. <br>
Esistono dei modelli statistici per il calcolo del costo. Il modello statistico più semplice da considereare è una distribuzione di probabilità che dica la probabilità $$p_i $$ di trovare il record nella pagina i.

Il costo medio è quindi:

$$ (1 * p_1 + 2 * p_2 + ... + N * p_N) = \sum_{i=1}^N i * p_i $$

con i = numero di pagine lette, $$p_i $$ = probabilità che la tupla sia nella pagina i.

Occorre però disporre della distribuzione di probabilità, che nella maggiorparte dei casi non è disponbile. Quindi si utilizza l'ipotesi della distribuzione uniforme. La tupla ha la stessa probabilità di trovarsi in una qualsiasi pagina.

In questo caso la formula si cemplifica ($$\forall i p_i = 1 / N $$) e diventa 

$$\frac{1}{N} \sum_{i=0}^N i =  \frac{1}{N} * \frac{N ( N + 1)}{2} = \frac{N + 1}{2}$$

Il corso della ricerca con successo è quindi (N+1) / 2, circa metà delle pagine.
Il costo della ricerca con insuccesso è N.

Se utilizzo un'organizzazione ordinata (ordinamento su un attributo) cambia solo il costo della ricerca con insuccesso, infatti non ho bisogno di scorrere tutte le pagine, ma mi arresto quando ho superato il valore richiesto, diventanto in termini di costi uguale al costo della ricerca con sucesso.


Se x non fosse chiave? Allora dovremmo scorrere tutte le pagine, e un discorso analogo lo potremmo fare per i range (<,>, between). Con un costo N. Non andremmo in dettaglio


Gli accessi sequenziali hanno costi che sono ell'ordine del numero di pagine(caso migliore la metà delle pagine)

Questa organizzazione è troppo costosa se pensiamo a sistemi informativi con migliaia di pagina per le tabelle. 

<h3>Metodo di accesso tabellare</h3>
E' il metodo più importante, in quanto si avvele degli indici

Gli indici sono uno degli aspetti più importanti della progettazione fisica di un DB.

L'indice è una struttura separata dall'area primaria(aria che contiene i dati). 

Però prima di conoscere gli indici dovremmo conoscere i B-Tree.



