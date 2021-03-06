---
TOCTitle: Valutazione dei requisiti per la migrazione
Title: Valutazione dei requisiti per la migrazione
ms:assetid: 'cec07f45-dc52-4004-860b-5cc33e5fc209'
ms:contentKeyID: 18824785
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc747759(v=WS.10)'
---

Valutazione dei requisiti per la migrazione
===========================================

Le organizzazioni che distribuiscono RMS devono stabilire un piano di migrazione che minimizzi il tempo di inattività del server in modo che possano supportare scenari di manutenzione e di aggiornamento server senza interrompere l'accesso degli utenti al contenuto protetto con RMS. Poiché i database di configurazione e di registrazione precedenti possono essere utilizzati da RMS, la migrazione di RMS da un server a un altro dovrebbe avere un impatto minimo sull'organizzazione, se vengono utilizzate le procedure appropriate. Nello scenario di migrazione si presume di volere utilizzare i database esistenti; altrimenti, si eseguirebbe una nuova installazione di RMS.

Se il server RMS che si sostituisce utilizza un dispositivo di protezione hardware (HSM), come nCipher, è necessario trasferire la configurazione dell'HSM sul nuovo server prima di installare ed eseguire il provisioning di RMS sul server. Per istruzioni, vedere la documentazione fornita con il modulo di protezione hardware.

Prima della migrazione:

-   Assicurarsi che i database siano disponibili.
-   Decidere quali computer verranno utilizzati nella nuova installazione.

Per migrare l'installazione RMS, seguire questi passaggi:

1.  Eseguire il backup di tutti i componenti prima di iniziare la migrazione, il che comprende il backup dei database, delle chiavi private e dello stato del sistema.
2.  Assicurarsi che i database della precedente installazione RMS siano nel server del database che sarà utilizzato per la nuova distribuzione.
3.  Installare RMS ed eseguire il provisioning sui server appropriati, quindi specificare il percorso dei database.

Uno scenario comune che richiede la migrazione del server RMS è lo spostamento di una distribuzione RMS pilota a un ambiente di produzione. Per ulteriori informazioni su questo scenario, vedere “Migrazione di una distribuzione pilota in una distribuzione di produzione” in “Distribuzione di RMS”, in questa documentazione.
