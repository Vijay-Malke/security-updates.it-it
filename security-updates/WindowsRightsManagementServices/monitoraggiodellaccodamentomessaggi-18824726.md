---
TOCTitle: 'Monitoraggio dell''accodamento messaggi'
Title: 'Monitoraggio dell''accodamento messaggi'
ms:assetid: 'a7109399-3a84-4681-874b-f6ea1646b0a0'
ms:contentKeyID: 18824726
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc747716(v=WS.10)'
---

Monitoraggio dell'accodamento messaggi
======================================

Per l'invio degli eventi al database di registrazione, viene utilizzato Accodamento messaggi (anche noto come MSMQ). Ogni server front-end di RMS invia messaggi al servizio Accodamento messaggi (MSMQ) e il servizio listener di registrazione attività di ogni server front-end recupera i messaggi di registrazione attività dalla coda MSMQ e li scrive nel database di registrazione attività. Se il database di registrazione attività o il server database non è più disponibile oppure se il servizio listener di registrazione attività viene interrotto, tramite Accodamento messaggi, i messaggi vengono memorizzati nella coda. Se si prevede di bloccare il database di registrazione attività o il server database, è consigliabile interrompere innanzitutto il servizio listener di registrazione attività di ogni servizio front-end e quindi riavviare tale servizio dopo avere riavviato il database o il server database.

Se il database non funziona e il servizio listener di registrazione attività è ancora in funzione, non è possibile scrivere i messaggi di registrazione attività nel database. Tramite il servizio listener di registrazione attività, i messaggi verranno spostati in una coda MSMQ di messaggi non recapitabili fino a quando il database non tornerà disponibile e sarà possibile quindi scrivervi i nuovi messaggi di registrazione attività. I messaggi nella coda dei messaggi non recapitabili verranno automaticamente scritti nel database di registrazione attività. Per visualizzare ed eliminare i messaggi nella coda dei messaggi non recapitabili, attenersi alla seguente procedura.

1.  Aprire lo snap-in Gestione computer di Microsoft Management Console (MMC). A tale scopo, fare clic su **Start**, scegliere **Tutti i programmi**, fare clic su **Strumenti di amministrazione** e quindi su **Gestione computer**.
2.  Nel gruppo Servizi e applicazioni nella struttura della console, fare clic su Accodamento messaggi e quindi su Code private.
3.  Verranno visualizzate due code. Il nome di entrambe inizierà con "**drms\_logging**" seguito dal nome del cluster. Una delle code sarà denominata "**drms\_logging\_***&lt;nome del cluster&gt;***\_deadletter**". Si tratta della coda dei messaggi non recapitabili. Fare clic sul nome della coda e quindi su Messaggi coda.
4.  Fare doppio clic su ogni messaggio per visualizzarne le proprietà.
5.  Per eliminare la coda, fare clic con il pulsante destro del mouse su **Messaggi coda**, scegliere **Tutte le attività** e quindi fare clic su **Elimina contenuto**.

In base alla configurazione predefinita, tramite Accodamento messaggi, vengono memorizzati tutti i messaggi in coda fino a raggiungere il limite dello spazio di archiviazione disponibile nel server. Se viene utilizzato tutto lo spazio disponibile nel disco rigido, non è possibile elaborare le richieste del client tramite il server RMS. Per evitare questo problema, attenersi alla seguente procedura per limitare la quantità di spazio su disco utilizzata da MSMQ per l'accodamento.

1.  Aprire lo snap-in Gestione computer di Microsoft Management Console (MMC). A tale scopo, fare clic su Start, scegliere Tutti i programmi, fare clic su Strumenti di amministrazione e quindi su Gestione computer.
2.  Nel gruppo Servizi e applicazioni nella struttura della console, fare clic su Accodamento messaggi e quindi su Code private.
3.  Verranno visualizzate due code. Il nome di entrambe inizierà con "drms\_logging". Per ogni coda, effettuare le operazioni descritte di seguito.
    -   Scegliere Proprietà.
    -   Selezionare la casella di controllo Limita archiviazione messaggi a (KB) e quindi specificare la dimensione totale, in kilobyte, destinata alla memorizzazione dei messaggi nella coda.

Se una coda si riempie, i messaggi provenienti da RMS verranno eliminati e al Registro eventi sistema verrà inviato il messaggio seguente, associato all'ID evento 48:

"Impossibile inviare il contenitore proprietà al servizio Accodamento messaggi."

È consigliabile configurare gli strumenti per il monitoraggio del sistema in modo che, al verificarsi di questo evento, venga inviato un avviso che segnala la presenza di un problema con il database di registrazione attività.
