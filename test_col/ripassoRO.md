---
layout: post
title:  "Ripasso: Vettori, matrici e sistemi lineari"
---
## Vettori

Un vettore *v* a *n* componenti (o *n* dimensioni) è una n-tupla ordinata di numeri reali $$v = (v_1, v_2,..., v_n) $$; l'insieme di tutti i vettori a n componenti è indicato il simbolo $$\mathbb{R}^n$$. Le quantità $$v_1, v_2,..., v_n $$ sono detti componenti di v. Due vettori $$v = (v_1, v_2,..., v_n) $$ e $$w = (w_1, w_2,..., w_n) $$; sono uguali se e solo se $$ v_1 = w_1, v_2 = w_2,..., v_n = w_n$$.
Il vettore $$ (0, 0, ..., 0) = 0 $$ è detto *vettore nullo*. 

Si noti che l'insieme dei numeri reali $$\mathbb{R}$$ può essere visto come l'insme $$\mathbb{R}^1$$ dei vettori a una solo componente; nel calcolo vettoriale i numeri reali sono anche detti scalari.

### Operazioni e prorietà**
Per tutte le operazioni sotto descritte, useremo due vettori: $$v = (v_1, v_2,..., v_n) $$ e $$w = (w_1, w_2,..., w_n) $$. All'occorrenza, inseriremo dei valori reali per rendere il formalismo maggiornamente comprensibile.


#### Somma
La somma di due vettori è cosi definita:

$$ v + w = (v_1 + w_1, v_2 + w_2, ..., v_n + w_n)$$

Esempio in $$\mathbb{R}^3$$, (3,7,9) + (5, -2, 0) = (8, 5, 9).

#### Prodotto numero-vettore
Aggiungendo al vettore v, il numero $$ a \in \mathbb{R}$$, definiamo:

$$ a \cdot v = (a \cdot v_1,(a \cdot  v_2, ..., (a \cdot v_n) $$

In altre parole, moltiplichiamo il numero reale per ogni componente singolarmente.
Esempio in $$\mathbb{R}^4$$, $$ 3 \cdot (1,2,3,55) = (3, 6, 9, 165) $$

#### Modulo

Si definisce *modulo* di un vettore v il numero non negativo $$ \|v\| = \sqrt{v \cdot v} $$. Un vettore con un modulo pari a 1 è anche detto versore



#### Proprietà 

- Associativa della somma: Per ogni $$u,v,w \in \mathbb{R}^n $$

(u + v) + w = u + (v + w)

- Esistenza dell'elemento neutro

v + 0 = v

- Esistenza e unicità dell'opposto

v + (-v) = 0

- Proprietà commutativa della somma

v + w = w + v

- Esistenza dell'elemento neutro per il prodotto numero-vettore

$$ 1 \cdot v = v $$

- Proprietà distributive

$$ a \cdot (v + w ) = a \cdot v + a \cdot w $$

$$(a + b) \cdot v = a \cdot v + b \cdot v $$

- Legge di annullamento del prodotto: Si ha av = 0, solo se a = 0 o v = 0

- Opposto del vettore:
    - - (av) = (-a) v
    - - (av) = $$a \cdot (-v)$$
    - -v = $$ -1 \cdot v $$

Stuttura di spazio vettoriale. Un insieme V sul quale siano definite le operazioni di somma tra elementi di V e di prodotto tra un numero e un elemento di V, è detto spazio vettoriale (sll'insieme dei numeri R), se le due operazioni godono delle seguenti proprietà:
- Associativa della somma
- esistenza dell'elemento della somma e dell'opposto
- commutativa della somma
- esistenza dell'elelemento neutro del prodotto numero-vettore
- le proprietà distributive 

Uno spazio vettoriale V non deve necessariamente essere costituti da nuple di numeri reali; si possono definire spazi di ...

#### Prodotto Scalare 

$$ v \cdot w = v_1 w_1 + v_2 w_2 + ... + v_n w_n = \sum_{i=1}^n v_i w_i $$

Si noti che il prodotto scalare ha come risultato un numero, e non un nuovo vettore. 

Esempio. In $$\mathbb{R}^3$$, $$ (2,4,6)\cdot (1, 3, 9) = 2 \cdot 1 + 4 \cdot 3 + 6 \cdot 9 = 68 $$

Sul prodotto scalare vale la proprieta commutativa e distributiva viste sopra. Per chi ha cazzi, esiste anche la dimostrazione.

# Geometria dei vettori nello spazio

I vettori in R^2 e in R^3 hanno una corrispondenza immediata con i punti del piano R^2 o dello spazio R^3: fissato un origine e un'unità di misura, le componenti di un vettore v identificano univocamente un punto nel piano o nello spazio. Graficamente, la rappresentazione è data dal punto stesso o da un segmento orientato, diretto dall'origine al punto stesso come mostrato i Figura

[Prendere l'immagine]


Somma vettoriale. La definizione della somma di vettori rispetta la regola del parallelogramma usata spesso in fisica per la somma dei vettori-forze: per sommare due vetori v e w si tracia il parallelogramma che per i lati v e w, e il vettore somma è la diagonale tesa tra l'origine e ed il vertice del parallelogramma ad essa opposto.

Il vettore-diagonale u è la somma risultante da v + w. 


