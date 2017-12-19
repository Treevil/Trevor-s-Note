---
layout: page
title: RO
permalink: /ro/
---

Disciplica dell'applicazione di metodi avanzati di analisi per aiutare a prendere desioni migliori.(www.informs.org)

Studia, progetta ed impiega modelli matematici, metodi quantitativi, strumenti software, simulazioni ed altre tecniche analitiche per affrontare e risolvere problemi complessi ed identificare le soluzioni.

Davanti ad un problema, crea un modello matematico per calcolarne una soluzione ottima o approssimarne una.

Testi/appunti
- Appunti (Grosso/Aringhieri).
- R. J. Vanderbei, Linear programming: foundations and extensions, (disponibile in rete).
- C. H. Papadimitriou,K. Steiglitz, Combinatorial optimization: algorithms and complexity.


## Toy Problem

Un gruppo di amici dovendo fare una gita ha deciso di mettere cibi e bevande in un unico zaino da **10Kg**. Lo zaino può essere iempito con:
- Cioccolata (conf. 500g)
- Succhi di frutta (bott da 1l)
- Lattine di birra (da 0.33l)
- Panini imbottiti (100g)
- Acqua minera (1l)
- Pacchi biscotti (500g)

Da un indagine fatta tra i partecipanti alla gita(si poteva dare un voto da 1 a 100 ad ogni progotto) sono stati determinati i seguienti punteggi:
- ciccolata 10
- succhi di frutta 30
- Lattine di birra 6
- Panini imbottiti 20
- Acqua minerale 20
- Pacchi di biscotti 8

Per non scontentate nessuno, si è deciso di portare
- 2 confezioni di cioccolata
- 2 bottlgie di succo di frutta
- 6 lattine di birra
- 10 panini
- 2 conf. biscotti

Formulare il modello di programmazione lineare che massimizzi il punteggio totale degli oggetti caricati nello zaino, rispettandone il vincolo di capacità.


### Soluzione

|   | Item        | Peso | Quant |
|---|-------------|------|-------|
| 1 | Cioccoalata | 1    | 2     |
| 2 | Succhi Fr.  | 2    | 2     |
| 3 | Birra       | 2    | 6     |
| 4 | Panini      | 4.0  | 40    |
| 5 | Acqua       | 0.0  | 0     |
| 6 | Biscotti    | 1.0  | 2     |


Le variabili di controllo determinano la struttura della soluzione di un problema, permettendone la realizzazione. Quindi in questo case è naturale definire le variabili:

$$x_1, x_2, x_3,.., x_6 $$

Con $$X_i$$ = quantitità di alimento i  (1= cioccolata, 2 = succhi di frutta, ...)

Con questa scelta di varibiali si può ottenere il seguente modello, nella quale compaiono due serie di vincoli: 
- un vincolo relativo alla capacità dello zaio, che non può essere superata 
- vincoli relaztivi ai qantitativi minimi di alimenti da caricare

 $$max 10 x_1 + 30 x_2 + 6 x_3 + 20 x_4 + 20 x_5 + 8 x_6 $$

soggetto a 

 $$\frac{1}{2} x_1 + x_2 + \frac{1}{3} x_3 + \frac{1}{10} x_4 + x_5 + \frac{1}{2} x_6 \leq 10 $$

$$ x_1 \geq 2; x_2 \geq 2; x_3 \geq 6; x_4 \geq 10; x_6 \geq 2 $$

$$ x_1, x_2, x_3, x_4, x_5, x_6 \in \mathbb{Z}_+ $$
<!-- 
|   | Item        | Quant | Peso | Profitto |
|---|-------------|-------|------|----------|
| 1 | Cioccoalata | 2     | 1    | 20       |
| 2 | Succhi Fr.  | 2     | 2    | 60       |
| 3 | Birra       | 6     | 2    | 36       |
| 4 | Panini      | 40    | 4.0  | 800      |
| 5 | Acqua       | 0     | 0.0  | 0        |
| 6 | Biscotti    | 2     | 1.0  | 16       |
|   | Totale      |       | 10   | 932      | -->

## Pianificazione della produzione

Un'azienda produce tre modelli 1, 2  e 3 di un certo prodotto. Ciascun modello richiede, due tipi di materiali grezzi (A e B) di cui sono dsiponibili rispettivamente 4000 e 6000 unità. In particolare, per produrre una nunità del modello 1 sono necessarie 2 unità di B; per una unità del modello 2 sono necessarie 3 unità di A e 2 unità di B; per una unitità del modello 3 sono necessarie 5 unitità di A e 7 di B. 

Il modelo 1 richiede, per ogni unità prodotta, il doppio di forza lavoro rispetto al modello 2 e il triplo rispetto al modello 3. La forza lavoro presente in azienda è in grado di produrre al massimo l'equivalente di 700 unità/giorno del modello 1. 

Il settore marketing dell'azienda ha reso noto che la domanda minima per ciascuno modello è rispettivamente di 200, 200 e 150 unità. Il profitto unnitario di ogni modello è di 30, 20 e 50 euro, rispettivmente. 

Formulare il programma lineare per pianificare la produzione giornaliera massimizzando il profitto.


### Soluzione

Le variabili saranno i 3 modelli: $$x_1, x_2, x_3 $$

$$ max 30 x_1 + 20 x_2 + 50 x_3 $$

soggetto a

1) $$ 2 x_1 + 3 x_2 + 5 x_3 \leq 4000$$
   $$ 4 x_1 + 2 x_2 + 7 x_3 \leq 6000 $$

2) $$ x_1 + \frac{1}{2} x_2 + \frac{1}{3} x_3 $$

3)$$ x_1 \geq 200; x_2 \geq 200; x_3 \geq 150 $$

$$ x_1, x_2, x_3 \in \mathbb{Z}_+ $$
