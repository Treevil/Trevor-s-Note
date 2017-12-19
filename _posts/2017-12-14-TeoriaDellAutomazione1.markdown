---
layout: post
title:  "Teoria dell'automazione: Intro"
date:   2017-12-14 08:18:49 +0100
categories: Linguaggi
---

Benvenuto a questa nuova serie di post sulla teoria dell'automazione. Questo corso parlerà delle grandi idee dietro l'informatica. 

<h3>Cos'è l'informatica?</h3>
L'informatica è molto di più della semplice programmazione. Edsger Dijkstra, vincitore de Turing Award, ed uomo estremamente dogmatico disse famosamente che l'informatica riguarda tanto i computer quanto l'astonomia riguarda i telescopi. Noi definiamo l'informatica come un set di strumenti matematici o un corpo di idee, per capire ogni sistema: il cevello, l'universo, gli organismi viventi e ovviamente... i computer. 

Forse avete iniziato la programmazione perché volevate capire i videogiochi, come ha fatto il sottoscritto. Beh, col tempo potrebbe esservi chiaro che capire i video giochi, vuol dire caprie l'universo. D'altro cos'è l'universo, se non un videogioco estremamente estremamente realistico?

OK, voi potreste dichiervi... ma se voglio capire l'universo non dovrei studiare fisica? Beh, i fisici hanno quello che si potrebbe definire un approccio top-down. Cerchi delle regolarità e provi ad incapsularle come leggi generali. 

Nell'infromatica lavoriamo nella direzione ooposta. Compiciamo con il sistema più semplice possibile, un insieme di regole che non sono state necessariamente confermate da esperimenti, ma che noi diamo per vere, e poi ci chiediamo quali tipo di sistema complesso noi possiamo e non possiamo costruire.

more: https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-045j-automata-computability-and-complexity-spring-2011/lecture-notes/MIT6_045JS11_lec01.pdf



La teoria dell'automazione è lo studio di computer astratti.
La prima versione si può ricondurre agli anni 30 quando A. Turin definito una macchina astratta chiamata *Turing Machine* con tutte le capacità dei moderni computer, a livello di elaborazione. Lo scopo di Turin era definire in modo preciso i limiti di quello che una macchina potesse fare o cosa non potesse fare. Le sue conclusioni sono ancora rilevanti oggi.

Negli anni 40/50 è stato introddotto un tipo più semplice di macchina, che oggi viene definito come automa finito. Questi modelli erano orignariamente pensati come simulazioni del cervello, si sono rivelati estremamente utili per altri presupposti. 

Verso il fine degli anni 50, C. Chmsky ha iniziato a studiare le grammatiche formali. Queste grammatiche hanno un importante relazione con i moderni linguaggi di programmazione. 

Nel 69, Cook estende gli studi di Turing su quello che non può essere calcolato. Separando i problemi che possono essere risolvibili dai computer in modo effficiente da quelli che in teoria potrebbero essere risolti ma in pratica richiederebbero uno sforzo computazionale così grande da essere praticamente irrisolbili se non per piccole istanze del problema. Questa classa di problema viene definita NP.

<h3>Motivazione</h3>
Per quale motivo dovremmo studiare la toria dell'automazione? Beh, perché questa toria a diversi impatti pratici su diversi settori. Ad esempio, gli Automi a stati finiti hanno trovato impiego nel:
- Software per il design e il controllo del compotamento dei circuiti digitali
- Lo sviluppo di Analizzatori Lessicali
- Software per la scansione di larghe quantità di testo
- Software di verifica dei sistemi 




<h3>Concetti Centrali</h3>
Prima di iniziare lo studio dell'automazione, è necessario che conosciamo i termini necessari per capire i post successivi.

Quando parilaimo di **Alfabeto**, intendiamo un insieme, non vuoto, di caratteri. Trandizionalmente indicato col carattere $$\Sigma $$ (sigma). 
Un paio di esempi:
- $$\Sigma = \{0,1\} $$ L'alfabeto binario
- $$\Sigma = \{a,b,..,z\}$$ insieme tutti i simboli minuscoli
- $$\Sigma = \{あ, い, う, え, お,...\}$$ l'insieme degli hiragana giapponesi
- L'insieme dei simboli ASCII. 

Quando invece si parla di stringhe **Stringhe**, parliamo di una sequenza finita di simboli scelta su un alfabeto. Ad esempio 1011 è una stringa sull'alfabeto dei binari.
La stirnga è *vuota* quando non contiene simboli, ed è denotata con $$ \epsilon$$, <br>
La *Lunghezza* di una stringa è il numero di caratteri di cui è composta la stringa. Quindi |1011| è di lunghezza 4, mentre $$| \epsilon | = 0$$. Se volessimo essere un po' piglioli, dire che la lunghezza di una stringa è il numero di caratteri non è esatto. In quanto con un alfabeto binario per quanto sia "lunga" la stringa abbiamo sempre e solo un numero di caratteri pari a due. Sarebbe più giusto dire il numero di posizioni all'interno della stringa. Non si usa questa definizione per amore della comprensione generale. <br>
L'operazione di *Concetenazione* tra stringe è quando si uniscono in successione 2 o più stringe. Detto più formalmente. Siano date le stringhe x, xy determinerà la concatenazione della stringha formata copiando tutti i caratteri di x seguiti da una copia di tutti ii caratteri di y. Più precisamente se x è formato al carattere a1, a,2,..., an, mentre y è formato dai caratteri b1, b2, ..., bi. Allora xy sarà a1, a2,..an, b1, b2,.., bi. 


*Potenza di un alfabeto*: Se $$\Sigma $$ è un alfaberto, possiamo esprimere l'insieme di tutte le stringhe di una certa lunghezza tramite la notazione di potenza esemoio

$$
\Sigma^0= \{\epsilon\}
$$

$$
\Sigma^1= \{0,1\}
$$

$$
\Sigma^2= \{00,01,10,11\}
$$

$$
\Sigma^3= \{000,001,010,100,011,101,110,111\}
$$


**Linguaggi**: Dato un alfabeto $$ \Sigma$$. Qualunque insieme L di stringe sull'alfabeto $$\Sigma (L \in \Sigma^*)$$ è un linguaggio su $$\Sigma$$

Anche un alfabeto può sempre essere visto come un linguaggio. Alcuni esempi di linguaggi possono essere: L'insieme delle parole italiane. L'insieme dei porgrammi C sintatticamente corretti. L'insieme delle stringhe che consistono di n zero seguiti da n uno, con un n maggiore di 0. {01, 0011, 000111,...}

Il linguaggio vuoto si deonota con [TODO].

<h4>Visione Insiemistica</h4>

Un linguaggio può essere definito mediante un descrittore di insiemi, del {w \| enunciato su w} <br>
Come {w | w consiste di un numero uguale di 0 e di 1} oppure {w | w è un numero binario primo}, ecc...

Spesso w viene sostiituito da un espressione con parametri e si descrivono le stringhe del linguaggio enuncianto le condizioni sui parametri, ed esempio: 

$$\{0^n 1^n | n \geq 1\} $$


Operazioni sui linguaggi:
- Unione
- Concatenazione
- Intersezione
- Potenze
- Chiusura di Kleene
- Chiusura positiva di Kleene 

[Esempio di utilizzo]

Proprietà delle operazioni sui linguaggi
- Unione
    - commutativa $$L \cup M = M \cup L $$
    - associativa $$(L \cup M)\cup N = L \cup (M \cup N) $$
    - elemeneto neutro $$\Phi \cup L = L $$
    - idempotente $$ L \cup L = L $$

- Concatenazione
    - associativa (L.M).N = L.(M.N)
    - elemento neutro  $$\epsilon . L = L$$
    - elemento zero $$\Phi .L = \Phi $$
    - distrubutiva a sinistra dell'unione $$L(M \cup N) = LM \cup LN$$
    - distributiva a destra dell'unione $$ (L \cup M).N = L.N \cup M.N $$

- Chiusura
    - Idempotente $$ (L^*)^* = L^* $$
    - $$ \Phi^* = {\espilon} $$
    - $${\epslion}^* = {\epsilon} $$
    - $$ L.L^* = L^*.L = L^+ $$
    - $$ L^+ = L^+ \cup {\epsilon} $$

**Problemi**
[Da prendere sul libro...]