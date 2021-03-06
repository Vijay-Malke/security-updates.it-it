---
TOCTitle: Database di configurazione RMS
Title: Database di configurazione RMS
ms:assetid: '769adbdc-f32f-464b-85c4-e8b160036187'
ms:contentKeyID: 18824661
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc747634(v=WS.10)'
---

Database di configurazione RMS
==============================

In RMS, viene impiegato un server database, ad esempio Microsoft® SQL Server o Microsoft SQL Server 2000 Desktop Engine (MSDE 2000) Release A, per memorizzare le informazioni relative a configurazione e norme. È presente un database di configurazione per ogni server o cluster RMS; esso memorizza, condivide e richiama i dati di configurazione e altri dati.

Il database di configurazione per il server o cluster di certificazione principale contiene un elenco di identità di utenti Windows, oltre ai rispettivi certificati per account con diritti. Prima di essere memorizzata nel database, la coppia di chiavi di certificazione viene crittografata nella chiave pubblica del server RMS. I database di configurazione dei server licenze non contengono queste informazioni.

Al gruppo del servizio RMS sono assegnate le autorizzazioni di esecuzione per le procedure presenti nel database.

**Importante   **È consigliabile utilizzare MSDE 2000 per supportare i database di RMS solo in ambienti di verifica, poiché MSDE 2000 non supporta alcuna interfaccia di rete. Inoltre, le condizioni per l'utilizzo di MSDE 2000 impediscono di utilizzare gli strumenti di SQL Server client per modificare un database di MSDE 2000. A causa di questa limitazione, non sarà possibile visualizzare informazioni sulla registrazione attività né modificare dati memorizzati nel database di configurazione.
