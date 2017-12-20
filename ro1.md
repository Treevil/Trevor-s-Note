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

## Il problema del distributore di giornali. 

La casa editrice ANALFABETA pubblica un quotidiano che viene distribuito da quattro centri di smistamento S1, S2, S3, S4 che richiedono rispettivamente almeno 100000, 150000, 50000 e 75000 copie. Il giornale viene stampato in tre tipografie T1, T2, T3 che producono rispettivamente al massimo 125000, 180000 e 70000 copie
I costi per la spedizione sono di 2 euro/Km. per giornale e le distanze tra le tipografie ed i centri di smistamento sono rispettivamente di 20, 25, 15 e 5 Km. per la prima tipografia, di 12, 14, 18 e 30 Km per la seconda, e di 19, 11, 40 e 12 Km per la terza.

(a) Formulare il modello di Programmazione Lineare per pianificare le spedizioni a costo totale minimo.
(b) Si definisca il costo di approvvigionamento di un centro di smistamento come il costo totale delle spedizioni verso quel centro. Formulare il modello di Programmazione Lineare che minimizza il massimo costo di approvvigionamento.

### Soluzione

[Dopo]



## Il problema del persona di un motel
Un motel autostradale, dovendo garantire un serivizio continuato 24 ore su 24, ha bisogno di un numero minimo di inservienti per ogni ora del giorno secondo la seguente tabella.


Ora: Numero Minimo
2-6 : 4
6-10: 8
10-14: 10
14-18: 7
18-22: 12
22-02: 4

Ciascun inserviente lavora 8 ore consecutive al giorno

Formulare il modello di programmazione lineare per garantire la presenza richiesta utilizzando il minor numero possibile di inservienti.

### Soluzione

