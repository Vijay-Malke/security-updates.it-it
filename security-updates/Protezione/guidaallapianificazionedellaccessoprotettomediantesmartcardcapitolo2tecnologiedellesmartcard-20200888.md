---
TOCTitle: 'Guida alla pianificazione dell''accesso protetto mediante smart card - Capitolo 2 - Tecnologie delle smart card'
Title: 'Guida alla pianificazione dell''accesso protetto mediante smart card - Capitolo 2 - Tecnologie delle smart card'
ms:assetid: '717aeaa4-f0f6-4fde-8774-7df04a28ff64'
ms:contentKeyID: 20200888
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Dd536289(v=TechNet.10)'
---

Guida alla pianificazione dell'accesso protetto mediante smart card
===================================================================

### Capitolo 2 - Tecnologie delle smart card

Aggiornato: 25/5/2005

La memorizzazione dei dati in rete è un requisito fondamentale per la maggior parte delle organizzazioni. Spesso, le organizzazioni devono collegare a Internet reti contenenti dati riservati e proprietari, al fine di consentire la comunicazione e lo svolgimento delle attività lavorative. La spinta costante verso una maggiore connettività espone a gravi rischi per la sicurezza, poiché la maggior parte delle organizzazioni utilizza l'autenticazione basata su nome utente e password per autorizzare l'accesso alle risorse di rete.

Il capitolo 1, "Introduzione", evidenzia il principale problema di sicurezza relativo alle combinazioni di nome utente e password. Poiché i nomi utente non sono segreti, solo le password forniscono una reale protezione contro gli accessi indesiderati da parte di malintenzionati che tentino di impersonare un utente valido. La comprensione della vulnerabilità delle credenziali di nome utente e password ha portato a un aumento dell'interesse per i sistemi di autenticazione a due fattori.

##### In questa pagina

[](#edaa)[Autenticazione a due fattori](#edaa)
[](#ecaa)[Prerequisiti per l'implementazione](#ecaa)
[](#ebaa)[Scenario Woodgrove National Bank](#ebaa)
[](#eaaa)[Riepilogo](#eaaa)

### Autenticazione a due fattori

L'autenticazione a due fattori va oltre le limitazioni delle semplici combinazioni di nome utente e password e richiede all'utente di presentare un token univoco abbinato a un PIN. Esistono svariati modi per implementare l'autenticazione a due fattori e questo numero è destinato ad aumentare in futuro.

#### Token hardware

I token hardware costituiscono un metodo di autenticazione a due fattori nel quale gli utenti sono in possesso di un elemento fisico di autenticazione, ad esempio una chiave o una tessera magnetica. Questo componente hardware fornisce un semplice codice di autenticazione monouso, che solitamente viene modificato ogni 60 secondi. Per identificarsi e ottenere l'accesso, l'utente deve conoscere il PIN segreto abbinato al codice monouso.

I token hardware garantiscono molti dei vantaggi delle smart card, ma possono richiedere una pianificazione e un processo di distribuzione più complessi. Microsoft® Windows Server™ 2003 e Windows® XP non dispongono di supporto incorporato per i token hardware.

#### Smart card

Le smart card sono tessere in materiale plastico (simili a carte di credito) che contengono un microcomputer e una piccola quantità di memoria, in grado di memorizzare chiavi private e certificati di protezione X.509 al riparo da possibili intrusioni. Normalmente, le smart card dispongono di 32 o 64 KB di memoria EEPROM (Electrically Erasable Programmable Read Only Memory) e ROM (Read Only Memory), oltre a un solo KB di RAM. La memoria ROM contiene il sistema operativo della smart card, mentre la memoria EEPROM contiene la struttura di directory e file, l'applet di gestione dei PIN e il certificato di autenticazione. La RAM rappresenta la memoria di lavoro per le operazioni della tessera, ad esempio crittografia e decrittografia.

Per autenticarsi con un computer o su una connessione ad accesso remoto, l'utente deve inserire la smart card in un apposito lettore e immettere il proprio PIN. In nessun modo è possibile ottenere l'accesso utilizzando separatamente il PIN o la smart card. Gli attacchi a forza bruta verso i PIN delle smart card non sono possibili poiché è previsto il blocco delle smart card dopo ripetuti tentativi di accesso inserendo PIN errati. Solitamente i PIN sono formati da un massimo di otto caratteri, pertanto sono più facili da memorizzare rispetto a lunghe password composte da caratteri casuali. Le smart card sono il meccanismo di autenticazione a due fattori consigliato da Microsoft.

**Nota:** per i PIN delle smart card non è obbligatorio utilizzare sequenze numeriche. I kit di sviluppo per smart card permettono di specificare il numero di caratteri richiesti, siano essi alfabetici, numerici, maiuscoli, minuscoli o non alfanumerici.

Microsoft distribuisce smart card agli amministratori di dominio e per l'accesso remoto alle risorse di rete e promuove questa pratica come parte delle operazioni di difesa in profondità. Microsoft Consulting Services, Premier Support, il Servizio Clienti Microsoft, i partner Microsoft e altri fornitori di soluzioni consigliano l'uso di smart card per garantire l'accesso protetto alle risorse di rete.

L'elenco che segue evidenzia le operazioni necessarie per implementare una soluzione basata su smart card per gli amministratori di rete:

-   Abilitare i server di destinazione in modo che supportino l'accesso interattivo, secondario o con desktop remoto con account abilitati all'uso di smart card.

-   Identificare gli amministratori che devono utilizzare un account amministratore a livello di dominio abilitato all'uso di smart card.

-   Distribuire i lettori di smart card.

-   Sviluppare un processo sicuro per la distribuzione di smart card e la registrazione degli amministratori.

L'elenco che segue evidenzia la procedura necessaria per integrare una soluzione basata su smart card per l'accesso remoto.

-   Aggiornare i server di accesso remoto affinché supportino l'autenticazione tramite smart card.

-   Identificare gli utenti che devono usare le smart card per l'accesso remoto.

-   Distribuire i lettori di smart card.

-   Distribuire le smart card agli amministratori e registrare gli utenti remoti.

[](#mainsection)[Inizio pagina](#mainsection)

### Prerequisiti per l'implementazione

La distribuzione delle smart card richiede una corretta pianificazione, al fine di garantire che l'organizzazione prenda in considerazione tutti i relativi problemi prima di iniziare la fase di implementazione. Questa sezione esamina i prerequisiti più comuni, nonostante in ogni ambiente sia possibile incontrare requisiti aggiuntivi.

#### Identificazione degli account

L'identificazione degli utenti e dei gruppi che necessitano di un accesso mediante smart card è una parte importante della distribuzione delle smart card stesse.

**Nota:** questa fase può essere ignorata dalle organizzazioni che dispongono dei requisiti di protezione e dei fondi necessari per implementare l'accesso mediante smart card per tutti gli utenti.

Tra i gruppi e gli utenti che necessitano di smart card sono incluse le seguenti figure:

-   Amministratori di dominio per tutti i domini di un insieme di strutture

-   Amministratori di schema

-   Amministratori dell'organizzazione

-   Amministratori di database

-   Amministratori delle risorse umane

-   Utenti che si servono dell'accesso remoto

-   Utenti che dispongono dell'accesso con privilegi di utente o amministratore a risorse riservate, quali informazioni contabili o finanziarie

L'organizzazione può anche richiedere l'uso delle smart card per utenti e gruppi non compresi nel precedente elenco, ad esempio per i componenti del consiglio di amministrazione. L'identificazione preventiva di questi account aiuta a definire la portata del progetto e a controllare i costi.

Per identificare gli account critici, è necessario definire quando utilizzare le smart card. Ad esempio, una buona norma di protezione consiste nel fornire a ogni amministratore due diversi account utente, uno standard per le attività quotidiane come la posta elettronica e uno a livello di amministratore per la manutenzione dei server e altre attività di gestione. Normalmente, l'amministratore si connetterà utilizzando l'account a livello utente e userà il Servizio di accesso secondario per eseguire le attività di gestione. In alternativa, è possibile utilizzare il componente Desktop remoto per amministrazione di Windows Server 2003, che supporta l'accesso tramite smart card. Per ulteriori informazioni sugli account amministratore, consultare la sezione Identificazione degli account amministratore e dei gruppi di amministratori nel capitolo 3 "Utilizzo di smart card per la protezione degli account amministratore".

#### Supporto dell'infrastruttura per le smart card

Le smart card richiedono un'infrastruttura adatta supportata dal sistema operativo e dagli elementi di rete. Microsoft supporta le implementazioni di smart card che utilizzano i seguenti componenti:

-   Servizi certificati Microsoft o infrastruttura a chiave pubblica (PKI, Public Key Infrastructure) esterna

-   Modelli di certificato

-   Windows Server 2003

-   Servizio di directory Active Directory®

    -   Gruppi di protezione

    -   Criteri di gruppo

    -   Stazioni e agenti di registrazione

    -   Server Web di attivazione

-   Extensible Authentication Protocol–Transport Layer Security (EAP–TLS), necessari solamente per le soluzioni di accesso remoto

Tra gli altri componenti figurano stazioni e agenti di registrazione.

##### Infrastruttura a chiave pubblica

Le smart card richiedono una PKI per poter fornire certificati con coppie di chiavi pubbliche/private che consentano il mapping degli account in Active Directory. Questa PKI può essere implementata in due modi: fornendo l'infrastruttura interna dei certificati a un'organizzazione esterna oppure utilizzando i Servizi certificati di Windows Server 2003. Le organizzazioni possono appaltare, interamente o in parte, il processo di gestione dei certificati per le smart card.

Le organizzazioni finanziarie possono trarre beneficio dal collegamento delle PKI a un'autorità attendibile esterna per la verifica della posta elettronica e per garantire transazioni protette con le organizzazioni partner. Un approccio alternativo consiste nell'impiego dei Servizi certificati in Windows Server 2003 per la fornitura della PKI.

Per ulteriori informazioni sui Servizi certificati in Windows Server 2003, consultare il sito Web [Public Key Infrastructure for Windows Server 2003](http://www.microsoft.com/windowsserver2003/technologies/pki/default.mspx) all'indirizzo www.microsoft.com/windowsserver2003/technologies/pki/default.mspx (informazioni in lingua inglese).

La PKI deve prevedere un meccanismo in grado di gestire la revoca del certificato. La revoca è necessaria alla scadenza del certificato oppure quando un utente malintenzionato può averne compromessa l'affidabilità. Ogni certificato comprende l'ubicazione del proprio elenco di revoche di certificati (CRL, Certificate Revocation List). Per ulteriori informazioni sulla gestione della revoca dei certificati, vedere l'argomento [Manage Certificate Revocation](http://technet.microsoft.com/en-us/library/cc759178.aspx) all'indirizzo www.microsoft.com/resources/documentation/WindowsServ/2003/standard/proddocs/en-us/sag\_CS\_procs\_revocation.asp (informazioni in lingua inglese).

##### Modelli di certificato

Windows Server 2003 fornisce modelli di certificato specifici per l'emissione di certificati digitali da utilizzare nelle smart card. Questi certificati possono essere copiati e personalizzati al fine di soddisfare i requisiti dell'organizzazione. I tre modelli di certificati per le smart card sono elencati di seguito.

-   **Agente di registrazione**. Consente la richiesta di certificati per altri utenti da parte di un utente autorizzato.

-   **Utente con smart card**. Consente all'utente di connettersi mediante una smart card e di firmare la posta elettronica. Fornisce anche l'autenticazione del client.

-   **Accesso con smart card**. Permette all'utente di accedere mediante una smart card e fornisce l'autenticazione del client, ma non consente la firma della posta elettronica.

Windows Server 2003 Enterprise Edition include i modelli versione 2 (v2) che possono essere modificati ed estesi per fornire più funzionalità, quali accesso, messaggi elettronici firmati e crittografia dei file. È possibile anche estendere i modelli di certificato in modo da fornire informazioni aggiuntive richieste dall'organizzazione, quali dati di carattere medico o pensionistico. Windows Server 2003 Enterprise Edition supporta la registrazione automatica, che semplifica la gestione delle smart card nelle organizzazioni di grandi dimensioni. La richiesta di rinnovo di un certificato può essere firmata utilizzando il certificato corrente.

**Nota:** Microsoft raccomanda di aggiornare le PKI attuali di Windows Server 2003 a Windows Server 2003 con Service Pack 1 (SP1) in modo da sfruttare le nuove e migliorate funzionalità di protezione.

Per ulteriori informazioni sui modelli di certificato, vedere l'argomento [Certificate Templates](http://technet.microsoft.com/en-us/library/cc758496.aspx) all'indirizzo www.microsoft.com/resources/documentation/WindowsServ/2003/standard/proddocs/en-us/sag\_ct\_topnode.asp (informazioni in lingua inglese).

##### Windows Server 2003

Microsoft Windows 2000 Server supporta l'uso delle smart card per l'accesso remoto e l'autenticazione dell'amministratore esclusivamente per l'accesso alla console. Per implementare le smart card per gli amministratori, è necessario che i server gestiti eseguano Windows Server 2003, il quale supporta operazioni secondarie quali l'accesso con smart card tramite connessioni con protocollo desktop remoto (RDP, Remote Desktop Protocol). Questi requisiti di sistema operativo comprendono i controller di dominio. Per ulteriori informazioni sui requisiti, consultare il capitolo 3 "Utilizzo di smart card per la protezione degli account amministratore".

##### Active Directory

Active Directory è un componente chiave per la distribuzione delle smart card. Active Directory in Windows Server 2003 dispone del supporto incorporato per rendere effettivo l'accesso interattivo con smart card ed è in grado di eseguire il mapping degli account ai certificati. Questa funzionalità di mapping degli account utente ai certificati collega la chiave privata presente sulla smart card con il certificato presente in Active Directory. La presentazione di credenziali di smart card durante l'accesso richiede che Active Directory stabilisca una corrispondenza tra una smart card specifica e un unico account utente. Per ulteriori informazioni sul mapping dei certificati, vedere l'argomento [Map Certificates to User Accounts](http://technet.microsoft.com/en-us/library/cc736706.aspx) all'indirizzo www.microsoft.com/resources/documentation/WindowsServ/2003/all/deployguide/en-us/dssch\_pki\_cyek.asp (informazioni in lingua inglese).

Active Directory supporta anche i gruppi di protezione e i criteri di gruppo che consentono di semplificare la gestione del processo di accesso tramite smart card e la loro emissione.

###### Gruppi di protezione

Il processo di distribuzione e gestione delle smart card risulta molto più semplice se gli utenti vengono organizzati mediante gruppi di protezione presenti in Active Directory. Ad esempio, una tipica distribuzione di smart card può richiedere la creazione dei seguenti gruppi di protezione:

-   **Agenti di registrazione smart card**. Gli agenti di registrazione smart card sono responsabili della distribuzione delle smart card agli utenti. La sezione che segue illustra dettagliatamente gli agenti di registrazione.

-   **Gestione temporanea di smart card**. Il gruppo di gestione temporanea di smart card contiene tutti gli utenti autorizzati a ricevere una smart card, ma le cui smart card non sono ancora state registrate e attivate da un agente di registrazione.

-   **Utenti con smart card**. Questo gruppo contiene tutti gli utenti che hanno completato il processo di registrazione e che dispongono di una smart card attivata. L'agente di registrazione provvede a spostare gli utenti dal gruppo di gestione temporanea delle smart card al gruppo degli utenti con smart card.

-   **Eccezioni temporanee delle smart card**. Questo gruppo contiene gli utenti che necessitano di eccezioni temporanee ai requisiti delle smart card, ad esempio in caso di smarrimento o dimenticanza della propria smart card.

-   **Eccezioni permanenti delle smart card**. Questo gruppo contiene gli utenti che necessitano di eccezioni permanenti ai requisiti di accesso mediante smart card, ad esempio gli account che eseguono servizi o attività pianificate sui server oppure gli utenti che operano con sistemi operativi e dispositivi che non soddisfano i requisiti di accesso mediante smart card.

Per ulteriori informazioni sulla creazione dei gruppi, vedere l'argomento [Checklist: Creating a Group](http://technet.microsoft.com/en-us/library/cc738419.aspx) all'indirizzo www.microsoft.com/resources/documentation/WindowsServ/2003/standard/proddocs/en-us/sag\_adgroups\_checklist\_create\_group.asp (informazioni in lingua inglese).

###### Criteri di gruppo

I criteri di gruppo consentono di applicare le impostazioni di configurazione a più computer. È possibile configurare i requisiti per l'impiego di smart card per l'accesso interattivo all'interno di un oggetto Criteri di gruppo (GPO, Group Policy Object), quindi applicare tale GPO a unità organizzative o siti in Active Directory. Per ulteriori informazioni su come utilizzare i criteri di gruppo, consultare il capitolo 3 "Utilizzo di smart card per la protezione degli account amministratore".

##### Stazioni e agenti di registrazione

Per emettere le smart card o registrare gli utenti, l'organizzazione può servirsi di un'interfaccia basata sul Web tramite la quale gli utenti possono immettere le proprie credenziali e ottenere la smart card. Tuttavia, questa soluzione riduce sensibilmente il livello di protezione offerto dalle smart card in quanto questo è pari al livello di protezione delle credenziali immesse nell'interfaccia Web. La soluzione consigliata è di creare stazioni di registrazione e definire uno o più amministratori come agenti di registrazione.

**Nota:** le organizzazioni possono impiegare un'interfaccia Microsoft Management Console (MMC) oppure sviluppare applicazioni di attivazione proprie.

Una stazione di registrazione tipica è costituita da un computer cui sono collegati due lettori di smart card. Uno di essi permette l'accesso dell'agente di registrazione, mentre l'altro rilascia le nuove smart card agli utenti. Le stazioni di registrazione richiedono un certificato di registrazione e devono essere autorizzate ad accedere ai modelli di certificato. La stazione di registrazione ha un'impostazione dei criteri di gruppo che forza la disconnessione non appena l'agente di registrazione rimuove la propria smart card dal lettore.

L'amministratore designato svolge il ruolo di agente di registrazione e utilizza la propria smart card per accedere alla stazione di registrazione. Successivamente, apre la pagina Web dei Servizi certificati, verifica l'identità dell'utente, lo registra e rilascia la smart card registrata.

Le organizzazioni devono considerare attentamente il numero di stazioni di registrazione richieste e la loro ubicazione. L'organizzazione può collocare una stazione di registrazione all'interno degli uffici del proprio reparto di sicurezza, assieme all'entità preposta al rilascio di accessi a risorse o siti e di altri pass di sicurezza. Per velocizzare la distribuzione iniziale nell'ambito di organizzazioni di grandi dimensioni, i gruppi di agenti di registrazione possono utilizzare computer portatili come stazioni di registrazione mobili nelle filiali.

**Nota:** per ridurre il grado di complessità di gestione e controllare la registrazione delle smart card, si raccomanda di limitare il numero di agenti e stazioni di registrazione al minimo indispensabile necessario per la distribuzione.

##### Server Web di attivazione

Il server Web di attivazione è un componente personalizzato che consente agli utenti l'attivazione delle nuove smart card mediante la reimpostazione del PIN. Gli SDK (Software Development Kit) di alcuni fornitori dispongono di strumenti che agevolano la creazione del server Web di attivazione. Microsoft non fornisce alcun componente server di attivazione.

Per reimpostare il PIN, l'utente deve eseguire l'utilità provider del servizio di crittografia (CSP, Cryptographic Service Provider) che genera una stringa di richiesta esadecimale dalla smart card. L'utente immette la stringa di richiesta in un campo della pagina Web, quindi il server Web di attivazione genera una risposta. A questo punto, l'utente immette la risposta nell'apposito campo dell'utilità, la quale consente all'utente di impostare il PIN della smart card.

Anche il server Web di attivazione può far parte del processo di gestione. Gli operatori dell'help desk possono sfruttare questo processo per sbloccare smart card per cui è stato immesso troppe volte un PIN errato. In questo caso, l'utente legge la richiesta all'operatore dell'help desk, il quale fornisce la risposta generata.

##### EAP-TLS

Gli ambienti di protezione basati su certificati utilizzano il protocollo EAP-Transport Level Security (EAP-TLS) per fornire il metodo di determinazione delle chiavi e di autenticazione più complesso. EAP-TLS permette l'autenticazione reciproca, la negoziazione del metodo di crittografia e la determinazione delle chiavi crittografate tra client e autenticatore. Le specifiche RFC 2284 forniscono una descrizione dettagliata del protocollo EAP.

#### Valutazione delle smart card

Il fattore principale nella valutazione delle smart card consiste nel garantire che il modello scelto sia in grado di supportare la lunghezza di chiave pianificata. Windows Server 2003 supporta chiavi di certificato di lunghezza compresa tra 384 bit (bassa protezione) e 16.384 bit (protezione massima).

I certificati che utilizzano chiavi più lunghe garantiscono una maggiore protezione rispetto a quelli con chiavi più brevi; tuttavia, nel primo caso il tempo necessario per l'accesso mediante smart card aumenta in modo significativo. Inoltre, le limitazioni di memoria delle smart card limitano la lunghezza massima delle chiavi utilizzabili.

Le chiavi di certificato di lunghezza pari a 1.024 bit sono adatte alla protezione degli account amministratore o degli accessi remoti. Un certificato con una chiave di 1.024 bit occupa circa 2,5 KB di memoria sulla smart card. Tra gli altri requisiti di memoria vi sono il sistema operativo (16 KB), le applicazioni del fornitore della smart card come il programma CSP (8 KB) e la struttura di directory e file della smart card (4 KB). Pertanto, le smart card dotate di meno di 32 KB di memoria possono non essere adatte a memorizzare i certificati di accesso e a fornire le funzionalità richieste per estendere la soluzione basata su smart card.

Il secondo fattore da considerare è la disponibilità del supporto incorporato per Windows Server 2003 e Windows XP. Prima di acquistare le smart card, è necessario discutere i requisiti con il fornitore.

**Nota:** si consiglia di acquistare le smart card direttamente dai rispettivi fornitori. Microsoft non fornisce smart card.

Nonostante Windows XP e la famiglia di Windows Server 2003 dispongano di supporto incorporato per alcuni tipi di smart card, ne esistono di altri tipi con crittografia basata su RSA in grado di funzionare correttamente con questi sistemi operativi. Per i tipi di smart card il cui supporto non è compreso in modo nativo in Windows, il fornitore implementare un CSP per le smart card che utilizzano lo standard CryptoAPI.

Per ulteriori informazioni sulla valutazione delle smart card, vedere l'argomento [Evaluating Smart Cards and Readers](http://technet.microsoft.com/en-us/library/cc737337.aspx) all'indirizzo www.microsoft.com/technet/prodtechnol/windowsserver2003/library/DepKit/0eae38ec-d6e5-4ca7-96a3-42f2fd6c6e74.mspx (informazioni in lingua inglese).

##### Gestione dei PIN

L'utente può modificare il PIN di una smart card in qualsiasi momento mediante l'uso di un'utilità che consente al CSP di visualizzare la finestra di dialogo con il PIN della chiave privata. Successivamente, l'utente immette il vecchio PIN seguito dal nuovo PIN (da specificare due volte). Poiché gli utenti trovano più facile ricordare i PIN personalizzati, si consiglia di prevedere l'uso di strumenti che consentano loro di modificarli come più opportuno.

**Nota:** può essere necessario ricordare agli utenti di non impostare PIN che possano essere indovinati facilmente, quali date di nascita, targhe di vetture o numeri di telefono.

L'utente è responsabile della gestione del PIN tramite i metodi forniti dal CSP. I sistemi operativi Windows XP e Windows Server 2003 non forniscono la gestione diretta dei PIN. Per informazioni su strumenti e istruzioni di gestione dei PIN, contattare il fornitore delle smart card.

La maggior parte dei fornitori offre smart card che si integrano direttamente in Windows 2000 o versioni successive, senza richiedere ulteriori personalizzazioni o sviluppo. I produttori forniscono queste smart card con un PIN preimpostato; inoltre, esse possono comprendere alcune limitazioni, quali ad esempio la richiesta di reimpostare PIN al momento della registrazione. Tuttavia, molte aziende non considerano accettabile questa impostazione.

Per creare PIN più complessi e sicuri, utilizzare gli strumenti di gestione per fare in modo che gli utenti scelgano PIN di lunghezza compresa tra cinque e otto caratteri. Assicurarsi che il produttore di smart card selezionato supporti PIN di otto caratteri di lunghezza.

##### SDK per smart card

Microsoft non fornisce soluzioni pronte all'uso per la distribuzione di smart card. Pertanto, può essere necessario fornire una ulteriore personalizzazione qualora l'ambiente lo richieda.

I fornitori di smart card offrono SDK e strumenti di personalizzazione che consentono alle organizzazioni di personalizzare la distribuzione delle smart card. Ad esempio, gli sviluppatori possono impiegare un SDK per rilasciare smart card in uno stato di sospensione. Quando l'agente di registrazione rilascia la smart card, l'utente la attiva e ne modifica il PIN. Se si desidera sfruttare la maggiore protezione garantita da questo metodo, è necessario prevedere il costo della personalizzazione e dello sviluppo necessari.

#### Valutazione dei lettori di smart card

Il fattore principale per la selezione di un lettore di smart card adatto alle proprie esigenze consiste nello scegliere quello che soddisfa meglio i requisiti posti. Ad esempio, una moderna workstation posizionata sotto la scrivania dell'amministratore dispone di due o più porte USB, quindi la scelta più adatta ricade su un lettore di smart card USB. L'utente può posizionare il lettore accanto al monitor o in un'altra ubicazione adatta. Solitamente gli utenti che accedono mediante connessioni remote da computer portatili preferiscono lettori di smart card in formato PC Card.

Sul mercato sono disponibili tastiere con lettori di smart card che funzionano anche tramite interfaccia USB. Queste tastiere sono adatte all'uso su un unico computer, ma possono funzionare con più computer alloggiati in rack di server attraverso uno switch di tipo KVM (Keyboard Video Mouse) con connessione USB. In questo caso, si consiglia di verificare con il produttore se lo switch KVM impiegato supporta l'autenticazione delle smart card su più server.

Windows XP e la famiglia di Windows Server 2003 supportano i lettori di smart card elencati nella seguente tabella. Windows installa i driver necessari non appena viene rilevata la presenza dell'hardware Plug and Play del lettore di smart card.

**Nota:** Microsoft raccomanda di utilizzare lettori di smart card che abbiano ottenuto il certificato di compatibilità con Windows.

**Tabella 2.1: Lettori di smart card supportati da Windows Server 2003**

 
<table style="border:1px solid black;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Marca</th>
<th style="border:1px solid black;" >Modello</th>
<th style="border:1px solid black;" >Interfaccia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">American Express</td>
<td style="border:1px solid black;">GCR435</td>
<td style="border:1px solid black;">USB</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Bull</td>
<td style="border:1px solid black;">SmarTLP3</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Compaq</td>
<td style="border:1px solid black;">Serial reader</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Gemplus</td>
<td style="border:1px solid black;">GCR410P</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Gemplus</td>
<td style="border:1px solid black;">GPR400</td>
<td style="border:1px solid black;">PCMCIA</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Gemplus</td>
<td style="border:1px solid black;">GemPC430</td>
<td style="border:1px solid black;">USB</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Hewlett-Packard</td>
<td style="border:1px solid black;">ProtectTools</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Litronic</td>
<td style="border:1px solid black;">220P</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Schlumberger</td>
<td style="border:1px solid black;">Reflex 20</td>
<td style="border:1px solid black;">PCMCIA</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Schlumberger</td>
<td style="border:1px solid black;">Reflex 72</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Schlumberger</td>
<td style="border:1px solid black;">Reflex Lite</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">SConnection Manager Microsystems</td>
<td style="border:1px solid black;">SCR111</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">SConnection Manager Microsystems</td>
<td style="border:1px solid black;">SCR200</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">SConnection Manager Microsystems</td>
<td style="border:1px solid black;">SCR120</td>
<td style="border:1px solid black;">PCMCIA</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">SConnection Manager Microsystems</td>
<td style="border:1px solid black;">SCR300</td>
<td style="border:1px solid black;">USB</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Systemneeds</td>
<td style="border:1px solid black;">External</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Omnikey AG</td>
<td style="border:1px solid black;">2010</td>
<td style="border:1px solid black;">Seriale</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Omnikey AG</td>
<td style="border:1px solid black;">2020</td>
<td style="border:1px solid black;">USB</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Omnikey AG</td>
<td style="border:1px solid black;">4000</td>
<td style="border:1px solid black;">PCMCIA</td>
</tr>
</tbody>
</table>
  
**Nota:** i lettori di smart card che utilizzano l'interfaccia seriale richiedono il riavvio del computer dopo l'installazione. Questo requisito può risultare inaccettabile per la loro implementazione su server.
  
Microsoft non supporta e sconsiglia l'uso di lettori di smart card non Plug and Play. Per impiegare uno di questi lettori, è necessario ottenere le istruzioni di installazione (compreso il relativo software del driver di periferica) direttamente dal produttore del dispositivo.
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Scenario Woodgrove National Bank
  
Nei successivi capitoli di questa guida viene utilizzato lo scenario della Woodgrove National Bank a fini di esempio. La Woodgrove National Bank è una banca di investimenti internazionale fittizia che opera come società di intermediazione finanziaria per conto di clienti istituzionali, aziendali o governativi e singoli individui. Le sue attività includono sottoscrizione di titoli, vendite e contrattazioni, servizi di consulenza finanziaria, ricerche sugli investimenti, speculazioni e servizi di brokerage per istituti finanziari.
  
La Woodgrove National Bank ha in organico più di 15.000 dipendenti in oltre 60 sedi in tutto il mondo. Le sedi centrali (dove si trovano gli hub) impiegano migliaia di dipendenti e sono dislocate a New York (5.000 dipendenti), Londra (5.200 dipendenti) e Tokyo (500 dipendenti). Ogni sede hub supporta più uffici.
  
Anche se la Woodgrove National Bank presenta un ambiente di server misti Windows e UNIX, la sua infrastruttura utilizza una backbone Windows Server. Sono presenti 1.712 server Windows, la maggior parte dei quali esegue Windows Server 2003. Circa 100 di questi server sono connessi a Internet. Inoltre, all'interno dell'organizzazione vi sono 18.000 workstation e 2.000 computer portatili. L'organizzazione ha in corso un processo di standardizzazione su Windows XP Professional con SP2, mentre per i server lo standard è Windows Server 2003 con SP1.
  
La maggior parte dei server è ubicata in tre sedi centrali. L'organizzazione dispone di workstation e computer portatili distribuiti in tutte le sedi. I computer portatili vengono spesso traspostati da un Paese all'altro o tra più regioni. La Woodgrove National Bank utilizza Microsoft Systems Management Server 2003 per gestire i computer da scrivania e portatili e Microsoft Operations Manager (MOM) 2005 per gestire i server.
  
La Woodgrove National Bank deve rispettare i requisiti degli enti di controllo delle strutture finanziarie di ciascun Paese/regione in cui si trova a operare. Inoltre, è necessario anche rispettare tutte le normative di protezione dei dati e dimostrare una efficace sicurezza operativa.
  
Il resto di questo documento descrive le scelte di progettazione disponibili durante la pianificazione della distribuzione delle smart card per la Woodgrove National Bank.
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Riepilogo
  
Questo capitolo contiene considerazioni di base necessarie per la pianificazione delle soluzioni di autenticazione mediante smart card. Ciò comprende i prerequisiti, ad esempio PKI e Active Directory. Il capitolo evidenzia la necessità di valutare le smart card e i relativi lettori, illustra gli eventuali problemi di memoria delle smart card, la lunghezza della chiave e la gestione dei PIN. I capitoli successivi sono incentrati sugli aspetti univoci dell'impiego delle smart card per garantire la protezione degli account amministratore e degli accessi remoti alle risorse di rete.
  
##### Download
  
[![](images/Dd536289.icon_exe(it-it,TechNet.10).gif)Guida alla pianificazione del monitoraggio della protezione e della rilevazione degli attacchi](http://go.microsoft.com/fwlink/?linkid=41314)
  
[](#mainsection)[Inizio pagina](#mainsection)
