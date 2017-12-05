---
layout: post
title:  "Algebra Relazionale"
date:   2017-12-05 8:18:49 +0100
categories: DataBase
---

L'agebra relazionale è il modello d'interrogazione formalizato da Codd. 
Il padadigma algebrico è una costruzione procedurale, ovvero un elenco di passi per eseguire l'operazione). 

Esistono diversi operatori per gestire le basi dati secondo questo modello, alcuni di base altri derivati. Vediamoli insieme.

Operatore di base:
- Selezione
- Proiezione
- Prodotto Cartesiano
- Unione
- Differenza
- Ridenominazione
Operatori Derivati
- Intersezione
- Il Join (nelle sue varie forme)
- Il quoziente 


Questi operatori del'algebra relazione ricevono come argomenti delle relazioni e producono in output delle relazioni, chiamate anche relazioni virtuali

Ma ora vediamo più nel dettaglio queste operazioni. Per fare degli esempi ci appoggeremo a queste tabelle d'esempio:

Tabella 1

| COD  | Cognome   | Nome  | Residenza | AnnoNascita |
|------|-----------|-------|-----------|-------------|
| A102 | Necchi    | Luca  | TO        | 1950        |
| B372 | Rossingni | Piero | NO        | 1940        |
| B543 | Missoni   | Nadia | TO        | 1960        |
| B444 | Missoni   | Luigi | CV        | 2000        |
| S555 | Rossetti  | Gino  | AT        | 2010        |



<h3>Selezione</h3>
Data una relazione r su uno schema A, $$\sigma (r(a))$$ è l'operatore di selezione dove p è un predicato e r(A) è l''argomento dell'operatore.

Questo predicato può assumere due forme:
- $$A_i \theta Costante$$
- $$A_i \theta A_j$$

