---
layout: post
title:  "Normalizzazione: Parte 1"
date:   2017-12-06 1:18:49 +0100
categories: DataBase
---

Non vedevate l'ora di farvi uno spiegozzo teorico sulla normalizzazione? Bene, allora cominciamo.

La normalizzazione è un approccio validio per i database del modello relazionale.


Un database non normalizzato a diverse anomalie:
- Anomali di inserzione
- Anomalie di cancellazione
- Anomalie di update

Per quanto riguarda la leggibilità abbiamo problemi di:
- sinonimie
- omonimie

[Aggiungere dopo esempio]

Per ridurre al minimo queste anomalie dobbiamo fare un processo definito **normalizzazione**.


**Aprroccio scientifico del problema**
- Percezione del problema
    - Obiettivi di buona progettazione 
- Tassonomia dei fatti salienti
    - Anomalie di inserzione, cancellazione, update 
- Ricerca di una formalizzazione adeguata 
    - Dipendenze Funzionali
- Messa a punto di una teoria ben fondata 
- Conseguenze della teoria 
- Applicazioni della teoria 



<h3>Dipendenza funzionale</h3>
Data una relazione r(A), un sottoinsieme X di attributi di $$ A(X \subseteq A), $$ un altro sottoinsieme Y di attrivuti di $$ A(Y \subseteq A) $$, il vincolo di dipendenza funzionale $$ X \rightarrow Y $$ (X determina Y) se è soddisfatto se e solo se:

$$\forall t_1, t_2 \in r(t_1[X] =  t_2[X] \Rightarrow t_1[Y] = t_2[Y]) $$


<div class="example">
<h5>Esempio vincoli</h5>


<img src="{{ "/asset/img/database/dipendenze_exemple.png" | absolute_url }}" alt="dio">

<br>
<br>
<br>

Esami (<u>MATR</u>, NS, IS, CAP, CF, DN, <u>Co</u>, Vo, DE, CP, NP, Q, TU) <br>

Dipedenze funzionali: 
MATR -> NS, IS, CAP, CF, DN
CF -> MATR
IS -> CAP
MATR, Co -> Vo, DE, CP, NP
CP -> NP, Q
Q -> TU
</div>

Ci sono più modi di vedere la realtà, e di raggruppare le dipendenze funzionali. Alcune equivalenti, altri no.

DUe basi di dati, una progettata con i vincoli F', l'altra progettata con i vincoli F'', fanno evolvere lo stato della base dati esattamente nello stesso modo. 


<h3>La teoria di Armstrong</h3>
Utilizzare la sola definizione di vincolo di dipedenza per verificare le equivalenze può risultare molto pesante.  Conviene quindi usare la Teoria di Armstrong delle dipedendenze funzionali. 

Armstrong è riuscito a costruire una teoria assiomatica con la quale caratterizza la dipedenza funzionale. 

Assiomi
 - Riflessività $$ Y \subseteq X \Rightarrow X \rightarrow Y \$$
 - Unione $$ X \rightarrow Y, X \rightarrow Z \Rightarrow x \rightarrow YZ $$ con $$YZ = Y \bigcup Z$$   
 - Transitività $$X \rightarrow Y,  Y \rightarrow Z \Rightarrow X \rightarrow Z $$

Il vincolo della dipendenza funzionale è un modello (in senso matematico) della teoria di Armstrong. Un modello calza su una teoria (fitta la teoria), quando gli assiomi della teoria sono rispettati dal modello.

Teoria e modello:
- La teoria di Armstrong è la teoria della "->" (assimo di riflessività, unione, transitivitià)

Teorema:
- espansione: $$ X \rightarrow Y, W \Rightarrow WX \rightarrow WY$$ 
- decomposizione: $$ X \rightarrow YZ \Rightarrow X \rightarrow Y, X \rightarrow Z$$ 
- Peudo-Transitività: $$ X \rightarrow Y, WY \rightarrow Z \Rightarrow Z $$
- Prodotto $$ X \rightarrow Y, W \rightarrow Z \Rightarrow XW \rightarrow YZ  $$



**Attibuto estraneo**: Date le seguenti dipendenze funzionali:
- ABCD -> E
- B -> C (data o dedotta dalle dipendeze date - ad esempio per transività)

Allora C è un attributo estraneo e si può cancellare, la dipedenza è allora ABD -> E

<h3>Chiusura di un insieme F</h3> 

La chiusura di dipendenze funzionali F è un insieme di dipendenze funzionali F+ tali che ogni dipendenza funzionale f+ dell'insieme F+ sia derivabile da F. 
(l'insieme F+ è finito)


La chiusura ci da lo strumento formale per caratterizzare dal punto di vista teorico il concettto di equivalenza. Immaginiamo di avere un progettista P1 che individua le dipendenze F e un altro progettista P2 che individua le dipendenza G, dove G è sintatticamente diverso da F. 

P1 e P2 stanno dicendo la stessa cosa? Ovvero, F e G sono equivalenti?

Possiamo affermare che $$ F \equiv	G $$ se e solo se $$ F^+ = G^+ $$

Il problema che risulta complesso construire F+ e G+ per verificare l'equivalenza...

Fortunamente, esiste una proprietà che porta al medesimo risultato. 

Possiamo affermare che $$ F \equiv	G $$ se e solo se $$ F  \vdash G, G  \vdash F$$ <br>

$$  \vdash $$ significa che è deducibile.
$$ F  \vdash G, G  \vdash F$$ Indicano che presta una qualsiasi proprietà g di G, g è deducibile da F (e viceversa).

Completezza e correttezza della teoria di Amstrong
La teoria assiomatica di Armstrong è una teoria corretta e completa. 

Di conseguenza ragionare con gli assiomi di Armstrong è perfettamente equivalente a ragionare con i vincoli sulle relazioni.

Per correttezza s'intende che se ho un insieme di dipedenze funzionali F e posso dedurre X -> Y, allora preso un modello delle dipendenze funzionali F, si ha come logica conseguenza il vincolo X -> Y, allora preso un modello delle dipendenze funzionali F, si ha come logica conseguenza il vincolo X -> Y

 - Per modello in un insieme di dipendenze funzionali F, si indente una relazione con n-tuple che soddisfa i vincoli F
 - La correttezza si ha quanod tutte le dipendenze funzinali derivabili da F sono anche vincoli soddisfatti da tutti i modelli di F
 - La dismostrazione si fa per induzione.

 Se ho un insieme di vincoli di dipendenza funzionale e si verifica che per ogni modello di F si ha come logica conseguenza X -> Y, allora X -> Y è deducibile da F.

 Chiusura di un insieme di attributi <br>
 Dato un insieme di attributi A, sui cui è definito l'insieme di dipedenze funzionali F, dato un sottoinsieme $$ X \subset A $$, la chiusura $$X^+$$ di X è definita come 

 $$ X^+ = \{A_i | F \vdash X \rightarrow A_i \} $$




<h3>Algoritmo per il calcolo di X+</h3>

![esempio dot notazione]({{ "/asset/img/database/algoritmoxplus.png" | absolute_url }}){:class="img-responsive"}


