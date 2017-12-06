---
layout: post
title:  "Algebra Relazionale: Intro"
date:   2017-12-05 8:18:49 +0100
categories: DataBase
---

L'agebra relazionale è il modello d'interrogazione formalizato da Codd. 
Il padadigma algebrico è una costruzione procedurale, ovvero un elenco di passi per eseguire l'operazione). 

Esistono diversi operatori per gestire le basi dati secondo questo modello, alcuni di base altri derivati. Vediamoli insieme.

**Operatore di base**
- Selezione
- Proiezione
- Prodotto Cartesiano
- Unione
- Differenza
- Ridenominazione


**Operatori Derivati**
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
Questa operazione ci permette di selezione le tuple.
Data una relazione r su uno schema A, $$\sigma (r(a))$$ è l'operatore di selezione dove p è un predicato e r(A) è l''argomento dell'operatore.

Questo predicato può assumere due forme:

$$A_i \theta Costante$$

$$A_i \theta A_j$$

Dove $$ \theta $$ indica un confronto insiemistico come {$$=, \neg, >, \geq, <, \leq $$}.

Esempi possono essere $$\theta_{residenti='TO'} (Tabella Cittadini)$$ per elencare tutti i cittadini di Torino.

La cardinalità
$$0 \leq | \sigma_p (r(A)) | \leq |r(A) |$$

Note: Cardinalità 0 con relazione 0, cardinitlità |r(A)| quando è vero per tutte le tuple.


<h3>Proiezione</h3>
Data una relazione r(A) ed un insieme di di attributi  $$A_1,A_2,.. A_n $$ tutti appartenenti alla relazione R, l'operazione di proiezione $$\Phi$$ permette di selezionare le colonne che ci interessano.

Potrebbe sembrare che a prima vista la cardinalità di questo operatore sia sempre uguale alla Relazione di partenza, ma se togliendo delle colonne le tuple si ripetono, queste vengono eliminate per non generare ripetizioni. Quindi la cardinalità va da 0 al numero totale delle tuple sulla R(A)

<h3>Operatori insiemistici</h3>

Operatore Unione, intersezione e differenza. <br>
Questi operatori richiedono per defnizione che gli schemi delle relazioni argomento siano identici.

Quindi $$schema_1 (A) e schema_2(A)$$ 

Cardinalità dell'unione 
$$0 \leq | r_1 (A) \cup r_2(A) | \leq |r_1(A)| + |r_2(A)| $$


Cardinalità dell'intersezione 
$$0 \leq | r_1 (A) \cap r_2(A) | \leq min {|r_1(A)|, |r_2(A)|} $$

Cardinalità dell'unione 
$$0 \leq | r_1 (A) - r_2(A) | \leq |r_1(A)| $$


<h3> Ridenominazione </h3>
A volte il fatto che gli inziemi non abbiano lo stesso schema può essere un problema. Allora viene in nostro aiuto l'operatore rinominazione. 
Il suo compito è semplicemente quello di cambiar nome agli attributi (uno o più).

Attenzione, questo operatore non modifica la base dati, cambia solo il nome dei suoi attributi.

<h3>Prodotto Cartesiano</h3>
Date due relazioni $$r_1 (A) ed r_2 (B), con A \cap B = 0 $$ (aka non hanno attributi in comune), il prodotto cartesino $$r_1(A) x r_2(B)$$ produce come risultato una relazione r' con:

Schema: R' composto dall'unione degli schemi $$A \cup B $$
Istanza: Combinazione di tutte le tuple di r1 (A) con tutte le tuple di r_2 (B)

immagine di esempio

Il prodotto cartesinao gode della proprietà commutativa.

Cadinalità:  
$$ 0 \leq |r_1(A) X r_2(B)| = |r_1 (A)| * |r_2(B)|$$

r_1 ed r_2 sono insiemi di tuple, quindi le tuple sono tutte disguinte. 

<h3>L'operatore Quoziente</h3>
Dati due insiemi disguinti di attributi A e B, l'operatore derivato quoziente si definisce come:

$$r(A, B) \div s(B) = \Pi_A(r)-\Pi_A((\Pi_a(r) \times s) - r)$$

La sua cardinalità è: 

$$ |r(A,B) \div s(B)) \leq |\Pi_a (r)| \leq |r| $$

Questo operatore soddisfa le interrogazioni con "tutti". 
Ad esempio: 
- Quali persone hanno comprato in TUTTE le boutiques nella citta X?
- Quali studenti sono registrati in TUTTI i corsi del professore X?
- etc


