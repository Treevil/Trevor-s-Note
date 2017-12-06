---
layout: post
title:  "Transizioni"
date:   2017-12-06 1:18:49 +0100
categories: DataBase
---

Il DBMS intercettta le azioni delle applicazioni nei confronti della base di dati. Le applicazioni, inviaion richieste DML di SELECT, INSERT, DELETE, UPDATE. 

Un primo compito del DBMS è quello di gestire la concorrenza. Un secondo obbiettivo del DBMS è quello di garantire la considenza dei dati (Verifica e rispetto dei vincoli).


Lo stato del DB può essere modificato da INSERT, DELEETE e UPDATE. 
Queste modifiche possono essere accettate se vengono rispettiati i vincoli, altrimenti vengono respinte. 

Esempio: <br>
Ora prendiamo che un nuovo clienti entri sulla nostra applicazione bancaria per chiedere un mutuo. <br>
Un vincolo impone che il nostro cliente sia prorietario di un conto corrente per poter chiedere il finanziamento. <br>
Il cliente prova a chiedere il mutuo ma la base dati lo respinge dicendo che dev'essere proprietario di un conto. <br>
Il cliente prova registrarsi un conto corrente ma la base dati lo respinge lo stesso perché il suo codice fiscale non è presente nella tabella clienti.... <br>

Possono esserci delle situaizioni in cui i vincoli non consentono a singole istruzioni di modifica dello stato della base dati di essere eseguite.

Se invece si consente al DBMS di eseguire provvisoriamente l'isstruzione di modifica e di aspettare l'arrivo di successive istruzio che pongano rimedio alla situazione di violazione dei vincoli, alla fine possono concludere che lo stato del DBMS è corretto (soddisfa tutti i vincoli). Da qui il concetto di transazione.

La transizione è una unità di programma:
- Inizia con un begin transction che comunica al DBMS la richiesta di interazione con esso da parte dell'applicazione
- Il DBMS identifica l'inizio della tansazione Ti e la abbian in modo univoco con l'utente/applicazione che ne ha fatto richiesta.
- Il DBMS, nell'ambito di T_i, riceve dei comandi DML in sequenza e le abbina alla transazione.
- La terminazione è decisa dall'applicazione attraverso due comandi: Commit (accetta) o rollback (reject).

Proprietà Transazioni:
- Atomica: O eseguita interamente o niente
- Cosistente: Manteine la base dati consistente. 
- Isolata: Ogni transazione fa affidamento di essere l'unica ad agire sulla base dati
- Durabile (persistnete): Tutte le modifiche andate a buon fine denono essere persistenti.

Ciclo di vita di una transizione

![Immagini Join]({{ "/asset/img/transizioniLife.png" | absolute_url }}){:class="img-responsive"}
