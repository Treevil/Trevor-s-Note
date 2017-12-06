---
layout: post
title:  "Calcolo Relazionale"
date:   2017-12-06 1:18:49 +0100
categories: DataBase
---

Come se l'algebra relazionale non fosse tediosa abbastnaza, molti professori potrebbero divertirsi a rompere il cazzo pure sul calcolo relazionale.

Il calcolo relazione può essere su tuple con dichiarazione di range o calcolo sui domini. Noi tratteremo solo il primo caso( grazie a dio)

L'interrogazione è composta da 3 parti:

{T | L | F}

T : Target <br>
Indica le informazioni che vogliamo in uscita. 

L: Range List <br>
Introduce le variabili abbinate a tavole di base.

F: Formula <br>
Predicati del primo oridne costituito dai operatori: 
$$\wedge , \vee, \neg, \Rightarrow, \forall, \exists $$ 


Esempio:
Elencare i pazienti residenti a torino. <br>
{p.Nome, p.Cognome | p(PAZIENTI) | p.residenza='TO'}

