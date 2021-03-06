---
TOCTitle: 'Appendice A: Impostazioni principali da considerare'
Title: 'Appendice A: Impostazioni principali da considerare'
ms:assetid: '6b4fdfca-4c2c-47f6-8c92-de33a663ea03'
ms:contentKeyID: 20213251
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc163065(v=TechNet.10)'
---

Guida per la protezione di Windows XP
=====================================

### Appendice A: Impostazioni principali da considerare

Sebbene questa guida descriva molte contromisure e impostazioni di protezione, è importante capire che una parte di esse sono particolarmente importanti. Questa appendice evidenzia tali impostazioni; è possibile fare riferimento al capitolo pertinente per una spiegazione sulla funzione dell'impostazione e sulla sua importanza.

Le impostazioni che dovrebbero essere contenute in questo elenco potrebbero essere discusse a lungo. L'argomento è stato dettagliatamente esaminato e discusso da un gruppo di esperti di protezione Microsoft. In base alle proprie esigenze personali, è possibile che alcune impostazioni manchino, o che alcune di quelle elencate siano superflue. Ogni organizzazione ha un ambiente diverso con requisiti aziendali unici, per questo motivo è lecito aspettarsi opinioni divergenti sui problemi di protezione. Tuttavia, questo elenco può aiutare ad assegnare le corrette priorità alle attività relative alla protezione di computer dotati di Microsoft Windows.

##### In questa pagina

[](#ebaa)[Contromisure importanti](#ebaa)
[](#eaaa)[Impostazioni di protezione principali](#eaaa)

### Contromisure importanti

Importanti contromisure, non relative alle impostazioni di protezione, comprendono:

-   Mantenere i computer aggiornati per quanto riguarda i service pack e gli aggiornamenti rapidi utilizzando gli strumenti automatici per la verifica e la distribuzione.

-   Installare e configurare il software firewall distribuito o i criteri IPsec di organizzazione.

-   Distribuire e aggiornare il software antivirus.

-   Distribuire e aggiornare il software antispyware.

-   Utilizzare un account non privilegiato per le attività quotidiane. Utilizzare un account con i privilegi di amministratore unicamente per eseguire incarichi che richiedono dei privilegi elevati.

[](#mainsection)[Inizio pagina](#mainsection)

### Impostazioni di protezione principali

Le impostazioni di protezione principali disponibili in Microsoft Windows comprendono:

-   Le impostazioni del criterio password, descritte nel Capitolo 2, "Configurazione dell'infrastruttura per il dominio di Active Directory:"

    -   Imponi cronologia delle password

    -   Validità massima password

    -   Lunghezza minima password

    -   Le password devono essere conformi ai requisiti di complessità

    -   Consenti archiviazione password con crittografia reversibile per tutti gli utenti del dominio

-   Le impostazioni di assegnazione diritti utente, descritte nel Capitolo 3, "Impostazioni di protezione per i client Windows XP:"

    -   Accesso al computer dalla rete

    -   Agisci come parte del sistema operativo

    -   Consenti accesso locale

    -   Consenti accesso tramite Servizi terminal

-   Le impostazioni di Opzioni di protezione, descritte nel Capitolo 3, "Impostazioni di protezione per i client Windows XP:"

    -   Account: limitare l'uso locale di account con password vuote all'accesso alla console

    -   Membro di dominio: aggiunta crittografia o firma digitale ai dati del canale protetto (sempre)

    -   Membro di dominio: aggiunta crittografia o firma digitale ai dati del canale protetto (quando possibile)

    -   Membro di dominio: aggiunta crittografia o firma digitale ai dati del canale protetto (quando possibile)

    -   Membro di dominio: chiave di sessione avanzata (Windows 2000 o versioni successive)

    -   Accesso di rete: consenti conversione anonima SID/NOME

    -   Accesso di rete: non consentire l'enumerazione anonima degli account SAM

    -   Accesso di rete: non consentire l'enumerazione degli account e delle condivisioni SAM

    -   Accesso di rete: consenti l'accesso libero agli utenti anonimi

    -   Accesso di rete: percorsi del Registro di sistema ai quali è possibile accedere in modo remoto

    -   Accesso di rete: limita accesso anonimo a named pipe e condivisioni

    -   Accesso di rete: condivisioni a cui è possibile accedere in modo anonimo

    -   Accesso di rete: modello di condivisione e protezione per gli account locali

    -   Protezione di rete: non memorizzare il valore hash di LAN Manager al prossimo cambio di password

    -   Protezione di rete: livello di autenticazione di LAN Manager

-   Le impostazioni aggiuntive del Registro di sistema, discusse nel Capitolo 3, "Impostazioni di protezione per i client Windows XP" soprattutto l'impostazione seguente:

    -   modalità di ricerca Safe DLL

##### Download

[![](images/Cc163065.icon_exe(it-it,TechNet.10).gif)Scaricare la Guida per la protezione di Windows XP](http://www.microsoft.com/downloads/details.aspx?familyid=2d3e25bc-f434-4cc6-a5a7-09a8a229f118&displaylang=en)

[](#mainsection)[Inizio pagina](#mainsection)
