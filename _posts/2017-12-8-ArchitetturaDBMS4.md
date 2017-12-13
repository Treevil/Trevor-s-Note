View Equivalenza

Supponiamo di avere due storie S1 e S2 dcon lo stesso insieme di transazioni.

Immaginiamo che ci sia un ipotetica transazione T0 che scrive i valori iniziali per ogni elemento del database letto da ogni transazione nelle storie e un altra ipotetica transazione Tf che legge ogni elemento scritto da una o più storie appena queste finiscono. 
 
 Allora per ogni azione di lettura ri(A) in una storia, possiamo trovare un azione wj(A) che ha preceduto la lettura in questione. Diciamo che Tj è la *fonte* della lettura di ri(A). Nota che la transizione Tj può essere l'ipotetica transizione iniziale T0 e Ti può essere Tf. 

 Se ogni azione di lettura in una storia è la fonte degli stesse altre storie, noi diciamo che S1 e S2 sono view-equivalenti. Sicuramente, storie view-equivalenti sono davvero equivalenti. Fanno le stesse cose che in ogni stato del database. Se la storia S è view-equivalente ad uno storia seriale, diciamo che è view-serializzabile. 

 Considera la storia S definita come:

| T1 |       |       | r1(A) |       | w1(B) |       |       |
| T2 | r2(B) | w2(A) |       |       |       | w2(B) |       |
| T3 |       |       |       | r3(A) |       |       | w3(B) |