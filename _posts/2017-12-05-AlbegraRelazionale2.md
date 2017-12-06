---
layout: post
title:  "Algebra Relazionale: Join"
date:   2017-12-05 14:18:49 +0100
categories: DataBase
---

In questo capitolo si apre la discussione sulle varie tipologie di Join.


<h3>Theta Join</h3>
Si usa per costruire informazioni combinando più relazioni. 

Date:
- due relazioni r_1(A) e r_2(B) con $$A \cap B = 0 $$
- Un predicato di join da intendersi come una congiunzione di confronti tra attributi.

Il $$\theta -Join$$ è definto come:
$$ r_1(A) r_2(B)= \sigma_\theta (r_1(A) X r_2(B)) $$

Cardinalità:
$$ 0 \leq | r_1(A) \Join_\sigma r_2(B) | \leq |r_1(A)| * |r_2(B)|$$


Attenzione però se due relazioni hanno un attributo con lo stsso nome se faccio un confronto questo creerà delle ambiguita. Quindi avremmo bisogno di sfuttare la rinominazione per toglierci dall'empase.

A volte poiché la rinominazioe appesantisce inutilmente la lettura delle esperessioni, posso utilizzare la dot notazione. Come nell'esempio.


![esempio dot notazione]({{ "/asset/img/dot-notazione.png" | absolute_url }}){:class="img-responsive"}

<h3> Equi Join </h3>
L'equi-join è un caso particolare di join, dove i confronti sono tutte uguaglianze. Si presenta con il simbolo 
$$ \Join_{\theta_e} $$


<h3>Natural join</h3>
Il natural join viene in nostro soccorso quando ci troviamo due tabelle sul quale vogliamo fare il Join che hanno lo stesso nome di attributo. 

In formule:

$$ r_1 (A) \Join r_2(B) = \Pi_{x,y,z} (r_1 )\Join_{\theta_e} \rho x' \rightarrow x (r_2))  $$

Il coaso è limite e quando abbiamo due schemi completamente disguinti, allora diventa equivalente al prodotto cartesiano.



<h3>Semi-Join</h3>

Date due relazioni r_1 (A) e r_2 (B), definiamo il semi-join come:

$$ r_1 (A) \ltimes_\theta	r_2(B) = \Pi_A (r_1(A) \Join_\theta r_2(B)) $$

L'operatore di semi-join funziona da selettore sulla prima tabella sfruttando la seconda tabella.


<h3>Outer Joint</h3>

![Immagini Join]({{ "/asset/img/join.png" | absolute_url }}){:class="img-responsive"}

Esistono 3 tipi diversi di Outer Join.
- Left Join  ⟕   	
- Right Join ⟖
- Full Join ⟗	
