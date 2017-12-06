---
layout: post
title:  "Algebra Relazionale: Aiuto Esecizi"
date:   2017-12-05 14:18:49 +0100
categories: DataBase
---

In questa sezione vediamo un po' di esempi su come risolvere gli esercizi più comuni sull'algebra relazione.

<h1>Conteggi</h1>
Come possiamo capire quantè volte è successa una certa cosa nell'algebra relazionale? 

In SQL questo si risolve facilmente tramite l'operatore COUNT. Ma in algebra relazionale dovremmo prendere una strada un po' diversa.

Possiamo mettere in join una relazione con se stessa e rinominare tutti gli attributi in modo che non ci siano ambiguità.

<h3>Interrogazioni Negative</h3>

Schema di risoluzione generale

1. Si definisce l'universo di interesse
2. Risponde alla domanda in forma positiva P
3. Trovo la risposta all'interrogazione R = U - P

Gli schemi di U e P devono essere uguali (e ovviamente compatibili) 