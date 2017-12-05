---
layout: post
title:  "Pendenza di una funzione"
date:   2017-12-04 22:18:49 +0100
categories: Analisi
---

Benvenuto nei miei appunti di analisi matematica,
questa pagina sarà dedicata alla lezione sulla pendenza di una funzione.

Come potreste aver gia visto le funzioni lineari sono rappresentate dalla formula, $$\ y = mx + q$$.

<p></p>Con un grafico che potrebbe essere qualcosa come:
![image-title-here]({{ "/asset/img/linea-retta.png" | absolute_url }}){:class="img-responsive"}


Possiamo lavorare su queste rette, e capire qual'è il loro  tasso di variazione, per convenzione chiamato delta, tramite queste semplici formule:
<p>
1) $$\Delta x = x_2 - x_1$$
2) $$\Delta f(x) = f(x_2) - f(x_1)$$
</p>

La prima per l'incremento di x, l'altra per l'incremento di f (o y).

Il quoziente è il tasso medio di variazione di f rispetto a x nell'intervallo tra [$$x_1$$, $$x_2$$], ricavabile con la formula:

$$ \frac{\Delta f}{\Delta x} = \frac{\Delta y}{\Delta x} = \frac{f(x_2) - f(x_1)}{x_2 - x_1}$$


**Teorema** 

Sia f(x) = mx + q, $$ x \in \mathbb{R} $$ <br />
con $$ m, q \in \mathbb{R} $$. Allora per ogni $$x_1 , x_2 \in \mathbb{R}$$ con $$ x_1 \neq x_2 $$ si ha

$$ \frac{\Delta f}{\Delta x} = m $$

Per le funzioni lineari, il rapporto $$ \frac{\Delta f}{\Delta x} $$ è constante indipendentemente dai punti scelti. 

**m**

Il valore *m* prende il nome di pendenza ed è il tasso medio di varazione di f in ogni intervallo. 

m è il coefficiente di prorzionalità diretta tra la veriazione assoluta di f e quella di x in un qualsiasi intervallo, ossia $$\Delta y = m \Delta x $$

Nel suo significato più intuitivo, la pendenza misura l'inclinazione del grafico della funzione. 
Salvo le funzioni lineare, la pendenza non è costante, basti pendenza al grafico di una funzione come x<sup>2</sup>. Quindi si parla di pendenza *in un punto*.

<h3>Come definire la pendenza di una funzione in un punto?</h3>

Condideriamo una funzione qualsiasi non lineare, prendiamo ad esempio la funzione f(x) = log(1 + 2x) e il punto c = 0. Nella figura sottostante sono riportati i grafici e un suo ingrandimento locale. 

![image-title-here]({{ "/asset/img/funzione_log1p2x.png" | absolute_url }}){:class="img-responsive"}

Se guardiamo da vicino il grafico attorno al punto (0,0) si vede una retta. 
La pendenza della funzione log(1 + 2x) nel punto ci è definita come la pendenza della retta che si vede ingradendo il grafico attorno al punto (0, 0). 

Abbiamo due modi per calcolare questa pendenza, *approssimato* ed uno *esatto*.

Nella versione approssimata ci basta scegliere un punto ad una distanza $$Delta x$$ e calcolare la pendenza secondo la formula nota:

$$ \frac{\Delta f}{\Delta x} = \frac{f(c + \Delta x) - f(c)}{\Delta x}{\Delta x} $$ con $${\Delta x \neg 0} $$

Mentre per un calcolo esatto dovremmo cercare di portare questo delta di più vicino possibile a 0. Per fare questo calcolo ci avverremo della nozione di limite:

$$ \lim_{\Delta x\to 0} \frac{f(c + \Delta x) - f(c)}{\Delta x}{\Delta x} $$

<h3>Quozione di Newton</h3>

Sia $$f: (c -r, c + r) \to \mathbb{R}, con $$c \in \mathbb{R} e r > 0 $$. Si chiama **quoziente di Newton** di f di base c un qualsiasi rapporto del tipo:
 
$$ \frac{\Delta y}{\Delta x} = \frac{f(c + \Delta x) - f(c)}{\Delta x}{\Delta x}$$ con $$\Delta x \neg 0 $$

Il limite infinitesimo (che tende a 0) della formula precedente, si chiama pendenza di f in c e la si denota con p(c), qualora esista questo limite finito.


<!-- @Aggiungere definizione precisa di tangente -->
