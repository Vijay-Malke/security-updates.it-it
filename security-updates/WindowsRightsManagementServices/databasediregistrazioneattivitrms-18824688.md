---
TOCTitle: Database di registrazione attività RMS
Title: Database di registrazione attività RMS
ms:assetid: '8ba147f3-16e4-4d9a-ac8f-f05ba2ba11bb'
ms:contentKeyID: 18824688
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc747669(v=WS.10)'
---

Database di registrazione attività RMS
======================================

Per ciascun cluster di certificazione o di licenza principale, nel programma di installazione di RMS viene installato un database di registrazione attività nella stessa istanza di server database server su cui è presente il database di configurazione. Il Programma di installazione crea inoltre una coda di messaggi privata per la registrazione attività in Accodamento messaggi. Il servizio listener per la registrazione attività trasmette dati da questa coda di messaggi al database di registrazione attività.

Al gruppo di servizi RMS sono assegnate le autorizzazioni di esecuzione per le procedure memorizzate che si trovano nel database di registrazione attività.

Poiché il servizio listener per la registrazione attività invia grandi quantità di dati al database di registrazione attività, è consigliabile impostare alcuni filtri in modo che nel database di registrazione attività vengano memorizzate solo le informazioni necessarie in una data organizzazione.
