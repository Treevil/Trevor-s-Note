---
layout: post
title:  "Algebra Relazionale: Esercizi Svolti"
date:   2017-12-05 8:18:49 +0100
categories: DataBase
---


Traduzione da: https://lagunita.stanford.edu/c4x/DB/RA/asset/opt-rel-algebra.html


Persona ( <u>Nome</u>, eta, genere ) <br>
Frequenta ( <u>Nome, pizzeria</u>) <br>
Mangia ( <u>Nome, pizza</u> ) <br>
Offre (<u>pizzeria, pizza,</u> prezzo )<br>

Write relational algebra expressions for the following nine queries. (Warning: some of the later queries are a bit challenging.)

Scrivi le espressioni in albegra relazionale per le seguenti queries. (Attenzione: Alcune delle ultime sono piuttosto una sfida)

1) Trova tutte le pizzerie frequentate da almeno una persona sotto i 18 anni.

$$ \Pi pizzeria (\sigma_{age < 18} (Persona \Join Frequenta)) $$

2) Trova il nome di tutte le femmine che mangiato la pizza ai funghi o al salame (o entrambe)

$$ \Pi Nomae \sigma_{genere="femmina" \wedge (pizza="salame" \vee pizza="funghi")}(Persona \Join Mangia)$$

3) Trova il nome di tutte le femmine che non mangiano sia pizza ai funghi che al salame

$$ \Pi Nome (\sigma_{pizza="funghi" \wedge genere="femmina"}(Persona \Join Mangia)) \enspace \cap $$
$$\Pi Nome (\sigma_{pizza="salame" \wedge genere="femmina"}(Persona \Join Mangia)))$$

4) Trova tutte le pizzerie che servono almeno una pizza che Amy mangia per meno di $10.00

$$\Pi pizzeria (\sigma_{nome="Amy"}(Mangia)  \Join \sigma_{price<10}(Offre))$$


5) Trova tutte le pizzerie che sono frequentate solo da femmine o solo da maschi 


$$ (\Pi pizzeria (\sigma_{genere="femmina"} (Persona) \Join (Frequenta)) - (\Pi pizzeria (\sigma_{genere="maschio"} (Persona) \Join (Frequenta)))) \cup $$
$$ (\Pi pizzeria (\sigma_{genere="maschio"} (Persona) \Join (Frequenta)) - (\Pi pizzeria (\sigma_{genere="femmina"} (Persona) \Join (Frequenta)))) $$


6) Per ogni persona, trova tutte le pizze che quella persona mangia che non sono servite delle pizzerie che quella persona frequenta. Restitusci tutte le coppie (nome di persona, pizza)

$$ Manga - \Pi Name, Pizza (Frequenta \Join Offre)$$

7) Trova i noma di tutte le persone che frequentano solo pizzerie che servono almeno una pizza che mangiano.


 $$ \Pi_{name} (Persone) - \Pi_{Name} (Frequenta - \Pi_{name, pizzeria} (Mangia \Join Offre)) $$


8) Trova i nomi di tutte le persona che che frenquentano ogni pizzeria che servono tutte le pizza che mangiano 

 $$ \Pi_{name} (Persone) - \Pi_{Name} (\Pi_{name, pizzeria} (Mangia \Join Offre)) - Frequenta $$


9) Trova la pizzeria che offfre la più economica pizza al salame. In caso di pareggi, restituire tutte le pizzerie.


[Continua]