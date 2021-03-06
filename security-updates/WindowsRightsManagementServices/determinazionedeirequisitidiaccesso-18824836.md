---
TOCTitle: Determinazione dei requisiti di accesso
Title: Determinazione dei requisiti di accesso
ms:assetid: 'eb2ce9a5-0430-4811-bd40-4a94a84426a8'
ms:contentKeyID: 18824836
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc747790(v=WS.10)'
---

Determinazione dei requisiti di accesso
=======================================

In questa sezione della fase di pianificazione, l'ambito dell'implementazione di RMS dovrebbe essere identificato. Nel valutare la protezione del sistema RMS, si dovrebbero prendere in considerazione i metodi da utilizzare per limitare l'ambito dei partecipanti e garantire che i dati protetti con RMS siano protetti anche attraverso le tradizionali procedure consigliate per la protezione delle informazioni. Ci si dovrebbe anche assicurare che l'accesso al server RMS per amministrazione e configurazione sia limitato ai soli amministratori attendibili. I metodi di protezione dell'accesso utilizzabili con RMS includono:

-   **Elenchi di controllo di accesso (ACL)**. Tutti i servizi Web RMS e il sito Web di Amministrazione possono essere protetti mediante elenchi ACL. Per essere certi che a utilizzare il servizio RMS siano solo gli utenti autorizzati, è possibile utilizzare gli elenchi di controllo di accesso per limitare la possibilità degli utenti di connettersi ai servizi RMS di certificazione e gestione licenze. Questo metodo può essere utile se si desidera che solo alcuni gruppi possano creare contenuto protetto o se si vuole consentire solo a determinati gruppi di ottenere licenze per il contenuto protetto.
-   **Autenticazione client**. È possibile anche richiedere che venga eseguita un'autenticazione mediante smart card o un altro tipo di autenticazione client quando un utente cerca di acquisire una licenza d'uso o un certificato. Questo metodo contribuisce a ridurre la possibilità che un utente non autorizzato apra i contenuti sfruttando la sessione di un utente autorizzato.
-   **Secure Sockets Layer**. Per fornire un livello di protezione aggiuntivo, è possibile anche richiedere una connessione SSL fra i client RMS e il server RMS. Si consiglia di abilitare SSL e richiedere la crittografia a 128 bit per ciascun file dei servizi Web RMS. Questi file hanno l'estensione .asmx e sono situati nelle directory virtuali Gestione licenze, Certificazione e Amministrazione. Se si desidera aprire le pagine Web **Amministrazione RMS** da un browser situato su un computer remoto, è necessario abilitare SSL. Tuttavia, anche se SSL è abilitato, non è possibile aprire la pagina **Amministrazione globale** da un computer remoto.
    Per informazioni sulla configurazione di SSL sui server, vedere la Guida di IIS.

Alcune organizzazioni necessitano di un sistema di gestione licenze dipartimentale, isolato dagli altri dipartimenti e protetto. In uno scenario di questo tipo, è possibile utilizzare un server RMS per istituire criteri di gestione dei diritti sulle informazioni. Se all'interno della propria organizzazione esiste un dipartimento o una divisione che controlla contenuti estremamente riservati, si può valutare l'opportunità di configurare un server o un cluster licenze separato per gestire la concessione in licenza e la pubblicazione dei contenuti in modo separato dal resto dell'organizzazione. Un server licenze è registrato in modo subordinato rispetto al server (o cluster) di certificazione principale, che fornisce a ciascun server licenze i servizi di certificazione e altri ancora. I server licenze, tuttavia, offrono propri servizi di gestione delle licenze e pubblicazione.

Gli account utente, gli elenchi ACL e la sicurezza fisica sono tutti elementi critici della distribuzione. Prima di implementare RMS in un ambiente di produzione, assicurarsi di aver valutato e implementato tutte le procedure ottimali di protezione e il proprio modello di protezione, secondo le necessità.
