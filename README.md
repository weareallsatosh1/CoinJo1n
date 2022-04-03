# CoinJo1n!

In sostanza, un CoinJoin comporta la combinazione di input da diversi utenti in una singola transazione. 
Prima di spiegare il come (e il perché), diamo un'occhiata alla struttura di una transazione normale. 
Le transazioni Bitcoin sono costituite da input e output. 
Quando un utente vuole effettuare una transazione, prende i suoi UTXO come input, specifica gli output e firma gli input. 
E' importante sottolineare che ciascun input viene firmato in modo indipendente, e gli utenti possono impostare output multipli (destinati a diversi indirizzi).

![01ebb344caee47eb807b6d3fa83f309e](https://user-images.githubusercontent.com/102928465/161452756-e8990ab3-ad6b-4ceb-8de9-42a846cc3504.png)


Se analizziamo una transazione composta da quattro input (0,2 BTC ciascuno) e due output (0,7 BTC e 0,09 BTC), possiamo fare alcune supposizioni. La prima è che stiamo guardando lo svolgimento di un pagamento – il mittente sta inviando uno degli output a qualcuno, e restituendo il resto a sé stesso. Dato che ha usato quattro input, l'output più grande è probabilmente per il ricevente. Nota che mancano 0,01 BTC negli output, corrispondenti alla commissione pagata ai miner. E' anche possibile che il mittente voglia creare una UTXO grande riunendo diverse più piccole, quindi consolida gli input più piccoli per ottenere il risultato desiderato di 0,7 BTC. Un'altra supposizione che possiamo fare si basa sul fatto che ogni input viene firmato in modo indipendente. Questa transazione potrebbe avere fino a quattro partecipanti diversi che firmano gli input, e qui troviamo il principio che rende efficaci i CoinJoin.

Come funziona il coinjoin

L'idea è che più parti si coordinano per creare una transazione, fornendo ciascuna gli input e gli output desiderati. Dato che tutti gli input vengono combinati, diventa impossibile dire con certezza quale output appartiene a quale utente. 

Considera il diagramma riportato sotto:

![3862b14074034f5ba73600717ff8e119](https://user-images.githubusercontent.com/102928465/161453155-ca850176-c4a6-4abb-926b-9c9170de68b7.png)


Qui, abbiamo quattro partecipanti che vogliono spezzare il collegamento tra transazioni. Si coordinano tra loro (o tramite un coordinatore dedicato) per annunciare gli input e gli output che vogliono includere.

Il coordinatore prenderà tutte le informazioni, le userà per creare una transazione, e farà firmare ogni partecipante prima di trasmetterla al network. Quando gli utenti hanno firmato, la transazione non può essere modificata senza diventare invalida. Quindi, non c'è il rischio che il coordinatore scappi con i soldi.

La transazione funziona come una sorta di scatola nera per mischiare monete. Ricorda che di fatto distruggiamo UTXO per crearne di nuove. L'unico collegamento tra le vecchie e le nuove UTXO che abbiamo è la transazione stessa, ma, ovviamente, non possiamo distinguere tra i partecipanti. Nella migliore delle ipotesi, possiamo dire che un partecipante ha fornito uno degli input e potrebbe forse essere il nuovo proprietario di un risultante output. Ma anche questo non è affatto garantito. Chi può dire, analizzando la transazione descritta sopra, che ci sono quattro partecipanti? Si tratta di una persona che invia i propri fondi a quattro suoi indirizzi? Due persone che effettuano due acquisti separati e restituiscono 0,2 BTC ciascuno nei propri indirizzi? Quattro persone che inviano a nuovi partecipanti, o rinviano indietro a sé stessi? Non possiamo esserne sicuri.

![Screenshot from 2022-04-04 00-20-41](https://user-images.githubusercontent.com/102928465/161453260-fa3258e5-1646-4e3a-a29c-a092b16dda72.png)

Come appare un coinjoin visto da un block explorer (blockstream)
    

