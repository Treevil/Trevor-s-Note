---
layout: post
title:  "Toc: Automi Finiti"
date:   2017-12-18 08:18:49 +0100
categories: Linguaggi
---

[Intro]



<h2>DFA</h2>
Ci sono molti sistemi o componenti di cui si può dire che in ogni istante si trovano in uno stato preso da un insieme finito. Uno stato ha lo scopo di ricordare una parte pertinente della storia del sistema. Con un numero finito di stati non si può in generale ricordare l'intera storia perchò il sistema deve essere progettato attentametne affinché ricordi ciò che è importante, dicmenticando ciò che non lo è. 

Il vantaggio di avere un numero finito di stati è che può essere implementato con un numero fissito di risorse. Come un circuito o un softare che prende decisioni basandosi su un numero limitato di dati.

[Definizione Informale]

Un automa deterministico finito è definito formalmente tramite una quintupla $$(Q, \Sigma , \delta , q_o, F)$$ dove:
- Q è l'insieme di tutti gli stati dell'automa
- $$\Sigma $$ è l'alfabeto
- $$\delta $$ è la funzione di transizione
- $$q_o  \in Q$$ è lo stato iniziale, e fa parte di Q. 
- $$ F  \subseteq Q$$ è l'insieme degli stati finali


Diagramma

Tabella di transizione

Estensione della funzione di transizione




![Immagini Join]({{ "/asset/img/then.svg" | absolute_url }}){:class="img-responsive"}


Formalmente, il linguaggio riconosciuto (o accettato) da DFA A è:

$$ L(A) = \{w | \hat{\delta}(q_o, w) \in F \}$$

I linguaggi riconosciuti (accettati) da automi a stati finiti sono chiamati **linguaggi regolari**. Due automi sono equivaleneit se accettano lo stesso linguaggio.

[Definizione formale di computazione - sispster]

[Esempio di esercizi]



<h2>NFA</h2>

[Definizione Informale]

Un automa non deterministico finito è definito formalmente tramite una quintupla $$(Q, \Sigma , \delta , q_o, F)$$ dove:
- Q è l'insieme di tutti gli stati dell'automa
- $$\Sigma $$ è l'alfabeto
- $$\delta $$ è la funzione di transizione
- $$q_o  \in Q$$ è lo stato iniziale, e fa parte di Q. 
- $$ F  \subseteq Q$$ è l'insieme degli stati finali


[Funzione di transizione estesa]


<h3>Conversione da NFA a DFA</h3>
Per quanto possa sembrare contro intuitivo, DFA e NFA hanno la capacità di riconoscere gli stessi linguaggi. Per ogni NFA A, è possibile construire un DFA B che riconosce lo stesso linguaggio. Generalmente il DFA ha lo stesso numero di stati del NFA di partenza, ma nel caso peggiore possiamo arrivare ad un DFA con $$2^n$$ per un NFA con n stati.

Esistono diverse tecniche di conversione, noi useremo il **subset construction**.

Questa tecnica comunica con un NFA N = $$(Q_N, \Sigma , \delta_N , q_o, F_N)$$ e il suo obbiettivo è costruire un DFA D = $$(Q_D, \Sigma , \delta_D , q_o, F_D)$$ tale che L(D) = L(N).

- $$Q_D$$ è l'insieme delle parti di $$ Q_N $$. Quindi se N ha n stati, D avrà $$2^n$$ stati. Spesso, non tutti questi stati sono raggiungibili, e quindi vengono eliminati durante il processo di costruizione del DFA.
- $$\Sigma$$ rimane invariato in entrambi gli automi
- Lo stato iniziale di D è lo stesso stato iniziale di N.
- $$F_D$$ è un insieme di sottoinsiemi di S di $$Q_N$$ tale che $$ S \cap F_N \neq \emptyset $$. In altre parole, $$F_D$$ è tutti gli insiemi degli stati N che includono almeno uno stato accettante di N. 
- Per ogni insieme $$ S \subseteq Q_N $$ e per ogni simboli di input $$ a \in \Sigma $$

$$ \delta_D(S,a) = \bigcup_{p \in S} \delta_N (p, q) $$

Questa dichiarazione formale potrebbe non essere chiarissima di primo impattto, ma sarà più chiara con un paio di esempi:


<h4>Un caso brutto per il subset construction</h4>


x
<h3>Epsilon Transizioni</h3>
Introduciamo una funzione in più, la capacità di spostarci tra gli stati con la stringa vuota, epsilon, senza leggere simboli di input. Questa funzione non espande il numero di linguaggi riconosciuti, ma ci da un modo di programmare gli automi conveniente in alcune situazioni.

[Esempio informale]

**Formalmente** rappresentiamo gli Epsilon-NFA come normali NFA con un unica eccezione, la funzione di transizione deve includere informazioni su epsilon. 

Vediamo $$\epsilon-$$NFA come A = $$(Q, \Sigma , \delta , q_o, F)$$ dove tutti i componenti hanno la stessa interpretazione del normale NFA, tranne che ora $$\delta$$ è una funzione che prende come argomenti: 
- Uno stato in Q
- Un membro di $$\Sigma \cup \epsilon$$. Stacchiamo l'alfabeto e epslion in modo che non ci sia confusione.

**La epsilon-chiura**.
Le epslion transizioni allargano anche la definizione di funzione di transizione estesa. Ma prima di vedere come cambia dobbiamo padroneggiare la nozione di $$\epsilon-$$chiusura. Informalmente, la $$\epsilon-$$chiusura di uno stato q, è l'insieme di stati che otteniamo quando seguiamo le sue esilon transizioni. 
La definizione formale richiede l'uso dell'induzione, ed essendo una vera rottura di coglioni per il momento la salto. 


**Funzione di transizione estesa** per le $$\epsilon-$$NFA è uguale a quella di un normale NFA, con l'aggiunta però che alla fine di analisi dell'input, facciamo la $$\epsilon-$$chiusura


<h4>Elimiazione delle Epsilon transizioni</h4>
Per ogni  $$\epsilon-$$NFA E, possiamo trovare un equivalente DFA D che accetta lo stesso linguaggio. La costruzione è molto vicina a quella fatta con il subset construction.



<h2>Minimizzazione</h2>
Concludiamo questa parte sugli automi studiando la loro minimizzazione.

